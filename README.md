# WOH-WOS-Analysis
* This is the calcualtion of "Weeks On Hand" / "Weeks Of Supply" (WOH/WOS) for the inventory analysis based on past sales, forecast, and monthly/weekly seasonality.  

## Description
* Internally, most of the item level weeks on hand are simply calculated as total inventory divided by weekly sales. However, Amazon Innetwork/DI orders in batches (B2B) which might overstate our true sales speed. To smooth out our weekly sales numbers, we should calculate our true weekly demand.
   - Non-AMZ DI_IN Weekly Sales: Last 12 weeks Non-AMZ_DI/IN weekly sales
   - AMZ DI_IN Weekly Sales: Last 12 weeks actual AMZ portal weekly sales
AMZ DI_IN Weekly Forecast: Next 12 weeks AMZ portal weekly forecast
IMT/OIT Forecast: Next 12 weeks HM forecast weekly sales 
OH_Days: Last 12 weeks number of days HM is on hand (>20pcs)
OH: Current US On Hand Inventory
OW: Current US On Water Inventory + Previous month planned but not yet shipped


## Getting Started

### Dependencies

* Describe any prerequisites, libraries, OS version, etc., needed before installing program.
* ex. Windows 10

### Installing

* How/where to download your program
* Any modifications needed to be made to files/folders

### Executing program

* How to run the program
* Step-by-step bullets
```
code blocks for commands
```

## Help

Any advise for common problems or issues.
```
command to run if program contains helper info
```

## Authors

Contributors names and contact info

ex. Dominique Pizzie  
ex. [@DomPizzie](https://twitter.com/dompizzie)

## Version History

* 0.2
    * Various bug fixes and optimizations
    * See [commit change]() or See [release history]()
* 0.1
    * Initial Release
