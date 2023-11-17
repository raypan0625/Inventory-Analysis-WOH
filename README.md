# WOH-Analysis
Calculation of "Weeks On Hand"/ "Weeks Of Supply" for the inventory analysis
Internally, most of the item level weeks on hand are simply calculated as total inventory divided by weekly sales. However, Amazon Innetwork/DI orders in batches (B2B) which might overstate our true sales speed. To smooth out our weekly sales numbers, we should calculate our true weekly demand.
