# Inventory-Analysis-WOH
* This is the comprehensive file for inventory analysis, inventory management, and promotion guidelines. The calcualtion of "Weeks On Hand" / "Weeks Of Supply" (WOH/WOS) for the inventory analysis is based on past sales, forecast, and monthly/weekly seasonality.  

## Description
* Internally, most of the item level weeks on hand are simply calculated as total inventory divided by weekly sales. However, Amazon Innetwork/DI orders in batches (B2B) which might overstate our true sales speed. To smooth out our weekly sales numbers, we should calculate our true weekly demand.
   - **Non-AMZ DI_IN Weekly Sales**: Last 12 weeks Non-AMZ_DI/IN weekly sales
   - **AMZ DI_IN Weekly Sales**: Last 12 weeks actual AMZ portal weekly sales
   - **AMZ DI_IN Weekly Forecast**: Next 12 weeks AMZ portal weekly forecast
   - **IMT/OIT Forecast**: Next 12 weeks HM forecast weekly sales 
   - **OH_Days**: Last 12 weeks number of days HM is on hand (>20pcs)
   - **updated_prod**: which month is the productivity score updated to, and change the productivity score included
   - **DNS_date**: Do not ship date, typically the first day of next month.
   - **Sellable qty in USA/On Hand(OH)**: sum of all available items of this product from all sources.
   - **On Water(OW)**: Current US On Water Inventory
   - **Pcs in shipping plan**: Pcs in the previous shipping plan that has not been shipped out
   - **On Order(OO)**: sum of quantity sent to factory for production and ready to be shipped out

## Calculations

### WOH_oos_sea  
Combine both seasonality and oos adjustment. Adjust for oos on Non-AMZ sales first then adjust seasonality on both Non-AMZ and AMZ Sales
   *	If OH Days < 30
         *	If non- AMZ DI Item:
Weekly Sales = Sum(Non-AMZ DI_IN Weekly Sales / OH_Days * 5 + AMZ DI_IN Weekly Sales) / Last 12 weeks Sales Weight * Next 12 weeks Sales Weight  
         *	If AMZ DI Item:
Weekly Sales = Sum(Non-AMZ DI_IN Weekly Sales / OH_Days * 5  + 0.3 * AMZ DI_IN Weekly Sales) / Last 12 weeks Sales Weight * Next 12 weeks Sales Weight

   *	If 72 >= OH Days >=30
         *	If non- AMZ DI Item:
Weekly Sales = Sum(Non-AMZ DI_IN Weekly Sales / OH_Days * 6 + AMZ DI_IN Weekly Sales) / Last 12 weeks Sales Weight * Next 12 weeks Sales Weight
         *	If AMZ DI Item:
Weekly Sales = Sum(Non-AMZ DI_IN Weekly Sales / OH_Days * 6 + 0.3 * AMZ DI_IN Weekly Sales) / Last 12 weeks Sales Weight * Next 12 weeks Sales Weight  

WOH_sea_oos = (OH+OW)/Weekly Sales_sea_oos_adj

### WOH_oos_sea new  
* All of the previous WOH calculations use inventory divided by average weekly sales. If the calculation period for average weekly sales is too long, the WOH won’t be very accurate for HMs with clear seasonality; if the calculation period is too short, any WOH that is longer than the calculation period won’t make much sense.	
* In this section, we introduce the most accurate calculation of WOH. For every future week, we will estimate sales adjusted for weekly seasonality and yearly growth. WOH is calculated by deducting each week’s sales from the current OH+OW inventory till it is fully depleted.
Assuming we are in wk 32,

| Week # | 20 - 31    | 32    |	33	| 34 | 35 | 36 | ...
| :---:   | :---: | :---: |:---: |:---: |:---: |:---: |:---: |
| Week % | 20.75%   | 1.73%|	1.84%|	1.88%|	2.08%	|1.62%|	…

WK 32 weekly sales = (Total WK 20-31 Non AMZ sales / OH_Days*(5 or 6) + (1 or 0.3)*Total AMZ)) / 20.75% * 1.73%  
WK 33 weekly sales = (Total WK 20-31 Non AMZ sales / OH_Days*(5 or 6) + (1 or 0.3)*Total AMZ)) / 20.75% * 1.84%  
WK 34 weekly sales = (Total WK 20-31 Non AMZ sales / OH_Days*(5 or 6) + (1 or 0.3)*Total AMZ)) / 20.75% * 1.88%  

```math
WOH = N - n + 1  where (OH_n + OW_n + Pcs in Shipping Plan_n)- \sum_{i=n}^N Week_i  Sales<0   
```

### WOH_oos_sea new yearly
This is linked to [Item-SKU Forecast](https://github.com/raypan0625/Item-SKU-Forecast)

* The basic idea is similar to WOH_oos_sea new. It is calculated by deducting each week’s sales from the current OH+OW inventory, and counting how many weeks it will take for the item’s stock to be fully depleted. But this method uses the yearly item level forecast, which is distributed to weekly sales based on weekly seasonality. This method of WOH calculation ties the forecast with the shipping plan and is the most up to date one. Refer to [Seasonality-Calculation](https://github.com/raypan0625/Seasonality-Calculation) for the weekly seasonality calculation method. The idea is the same but weekly seasonality will be using week numbers rather than months. Say we are in week 35 of 2023, then we’ll find all rolling 53 weeks with sales (week 35 of 2022-week 34 of 2023 , week 35 of 2021-week 34 of 2022, etc.).

## Other Measurements
### Estimated Next Ship Date & Estimated shipping qty at ship date
These measurements provide a guideline for the estimated next ship date and next ship qty, making necessary preparation for next shipment. 

*Lead time consideration: 1 month when shipping from China to US, 2 months when ship from other countries (Malaysia, India, etc.) to US*
### Estimated Next Reorder Date & Estimated Reorder qty at Reorder date
These measurements provide a guideline for the estimated next reorder date and next reorder qty, making necessary preparation for factory negotiation.

## Authors

Yulin Pan raypan0625@gmail.com

## Version History

* 0.1
    * Initial Release
