---
layout: left-menu
title: Load data
tagline: technical documentation for JDemetra+ using GitHub Pages
description: Upload the data
order: 10
---
# {{page.description}}

This part is not specific to the `Nowcasting plugin`. There are multiple ways to upload the data in JDemetra+. Let's explore two options:

- Load data from an Excel file. For instance, you can use the file [_GermanExample.xls_](https://github.com/nbbrd/jdemetra-nowcasting/wiki/Models_and_Data/DE/GermanExample.xlsx) that we have prepared and save it in your PC. If you want to use your own data file, it is crucial to make sure the dates are in the first column and the name of the series is in the first row.
- Load data from an SDMX file. This format is used by Eurostat to distribute most of its data. As an example, here you can download in SDMX-ML format a selection of business cycle indicators for the European Union:
	- [Unemployment level](https://open-data.europa.eu/en/data/dataset/HuhJ5kr24H1ymxpaDkamxA) 	
	- [HICP](https://open-data.europa.eu/en/data/dataset/eWEhQZ17tyHTWf7CdyHrA)
	- [Tourism number of nights spent](https://open-data.europa.eu/en/data/dataset/vRkVEpAUZQg9sbvTIhfGA)
	- [Volume of retail trade](https://open-data.europa.eu/en/data/dataset/7OJLyRVIeyVmhqbwtFdA)
	
This selection includes the variables that will be tracked in the [BDCOMP competition](http://fxdiebold.blogspot.be/2015/12/eurostat-forecasting-competition.html). 

Go the the Providers Tab, which is placed by default in the left-hand side of the window:

- Load your data (both in Excel and SDMX, although I will only use the Excel file)
 
 ![LoadDataGermanExample](https://github.com/nbbrd/jdemetra-nowcasting/wiki/images/LoadExcelSdmx.gif) 
 

- An unbreakable link between the model and the path of the excel file will be created at the precise moment when you drag and drop your data into your model space. If you want the nowcasting model to read the data from other file with the same name, or from the same file that has been moved to a different location, proceed as indicated in the next video: remove the path (choose a relative path if you prefer)
 
 ![RemovePath](https://github.com/nbbrd/jdemetra-nowcasting/wiki/images/RemovePath.gif) 
 

- Make sure the JDemetra+ environment knows the path where you are storing your data. When your source data is updated, 
you will be able to decide whether you want your models to read that new data with a simple `refresh` action. However, JDemetra+ may 
not find it if you have changed its location or if you are teleworking from home with a different machine. Go to the menu 
bar and click on `Tools`. Select `Options` and go to the tab _Demetra paths_. For each one of the data formats, you can specify the address 
where the JDemetra+ environment should start looking for the data.
 
 ![DemetraPaths](https://github.com/nbbrd/jdemetra-nowcasting/wiki/images/DemetraPaths.gif) 
 






