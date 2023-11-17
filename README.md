# WOH-WOS-Analysis
This is the calcualtion of "Weeks On Hand"/ "Weeks Of Supply" for the inventory analysis based on past sales, forecast, and monthly/weekly seasonality.  
Internally, most of the item level weeks on hand are simply calculated as total inventory divided by weekly sales. However, Amazon Innetwork/DI orders in batches (B2B) which might overstate our true sales speed. To smooth out our weekly sales numbers, we should calculate our true weekly demand.  

## Description

An in-depth paragraph about your project and overview of use.

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
