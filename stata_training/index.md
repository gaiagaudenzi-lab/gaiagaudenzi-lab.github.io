---
layout: default_subpages
title: Stata Training
---

# Stata training

This "Stata guide" is intended to be a handy resource for you, and you can use it the way you want. It is divided in topic but it is not consequential, meaning you can jump from one chapter to another without any problems. 

If you already have a knowledge of what Stata is, you can definitely skip the Stata basic part. I will try to cover from the very basic to the very advanced (as far as I know), but if you think I took something for granted, or something is not well explained shoot me a message! Feel free to copy and paste my code and send me an email at gaiagaudenzi9@gmail.com if you have problems working with the code! 

## What is Stata? 
Nothing else than a statistic software to analyze your data! It is widely used (at least in Economics, which is the field where I come from) and it is very simple to use. You can browse through this training to have a sense of what you can do with it and get used to the language and terminology. 
	
Here is an example of a Stata interface:

![Stata_interface]({{site.url}}/images/Stata1.png)
	
You should use the interface only to look at variables, at the output etc. you should NOT type from the command prompt. It is extremely inefficient to type your commands directly into the Command prompt. You should use dofiles instead! (We'll talk about them in a second).


## Stata basics 

The most important code in Stata is 

```stata
help
```
## Loading data and directories

How can you locate on your laptop the files you will load into Stata? With the directory of the file itself! For every file you import/load in Stata you have to specify the directory, to tell Stata where exactly it has to find the file. So, to load a .dta (the Stata format for databases) into Stata, you will use the following syntax:

```stata
      use "yourdirectory/dataset.dta"
```

To know in which directory you are at the moment, type

```stata
pwd
```
It will return the directory Stata is in. To change directory:

```stata
cd "otherdirectory"
```
To create directories:
 ```stata
mkdir "otherdirectory"
```

## Use dofiles! 

## Organize your workflow

## Globals and locals 

## Collaborative coding setting 

## Loading Data 

## Data cleaning 

 ```stata
    rename _all, lower 
    destring(var), replace
    tostring(var), replace 
```
### Identify missing values 
 ```stata
mvdecode _all, mv(99=.m \ 96=.d )</code>
```
### Cleaning strings 

## Data manipulation 

## Data visualization 

## Exporting Data 

# Selected topics in using Stata

## How to produce stunning summary statistics? 

## How to create maps?
Did you know you can create simple maps in Stata? This is thanks to the absolutely awesome people that invented the spmap command. 
```stata
* 1.8.2 Maps

* 1 STEP: Convert shapefile to .dta<br>

	shp2dta using "$training_data/4_Data visualization/Map/gadm36_BGD_2.shp", data("$training_data/4_Data visualization/Map/BGD_zilamap") coor("$training_data/4_Data visualization/Map/BGD_zilacoor") replace genid(id)<br>
	
	u "$training_data/4_Data visualization/Map/BGD_zilamap.dta", clear<br>
	
	spmap using "$training_data/4_Data visualization/Map/BGD_zilacoor.dta" , id(id) <br>

* Mark unfeasible districts<br>

	u "$training_data/4_Data visualization/Map/BGD_zilamap.dta", clear<br>

	* 1.1 Mark Hill tract areas<br>
	#delim ;<br>
	g var = "Hill tract/Cox's" <br>
	if NAME_2 == "Chittagong" <br>
	| NAME_2 == "Khagrachhari" <br>
	| NAME_2 == "Rangamati" <br>
	| NAME_2 == "Bandarban" <br>
	| NAME_2 == "Cox'S Bazar"<br>
	;<br>
	#delim cr<br>

	* 1.2 Mark Haor areas<br>
	#delim ;<br>
	replace var = "Haor areas" <br>
	if NAME_2 == "Sylhet" <br>
	| NAME_2 == "Maulvibazar" <br>
	| NAME_2 == "Habiganj" <br>
	| NAME_2 == "Sunamganj"<br>
	;<br>
	#delim cr<br>

	* 1.3 Mark areas affected by Cyclones<br>
	#delim ;<br>
	replace var = "Cyclones" <br>
	if NAME_2 == "Khulna" <br>
	| NAME_2 == "Bagerhat" <br>
	| NAME_2 == "Pirojpur" <br>
	| NAME_2 == "Jhalokati"<br>
	| NAME_2 == "Patuakhali"<br>
	| NAME_2 == "Barguna"<br>
	| NAME_2 == "Bhola"<br>
	| NAME_2 == "Noakhali" <br>
	| NAME_2 == "Satkhira"  <br>
	;<br>
	#delim cr<br>

	* 1.4 Mark areas affected by flooding<br>
	#delim ;<br>
	replace var = "Flooding" <br>
	if NAME_2 == "Faridpur" <br>
	| NAME_2 == "Sirajganj" <br>
	| NAME_2 == "Tangail" <br>
	| NAME_2 == "Jamalpur" <br>
	| NAME_2 == "Gaibandha" <br>
	| NAME_2 == "Lakshmipur" <br>
	;<br>
	#delim cr<br>

	* 1.5 Mark areas affected by water logging<br>
	replace var = "Water Logging" if NAME_2 == "Jessore" <br>

	* 1.6 Mark areas affected by flash flood (if not already eliminated)<br>
	replace var = "Flash flood" if NAME_2 == "Netrakona" <br>

	encode var, g(var2)<br>
	
	preserve<br>
	* Create labels (not compulsory) <br>
	u "$training_data/4_Data visualization/Map/BGD_zilacoor.dta", clear<br>
	collapse (mean) _X _Y, by(_ID)<br>
	rename _ID id<br>
	merge 1:1 id using "$training_data/4_Data visualization/Map/BGD_zilamap.dta"<br>
	keep id _X _Y NAME_2<br>
	save "$training_data/4_Data visualization/Map/BGD_label_coor", replace<br>
	restore<br>
	
	* 1.7 Create map<br>
	spmap var2 using "$training_data/4_Data visualization/Map/BGD_zilacoor.dta" , id(id) clmethod(unique)  ocolor(gs8 ..) fcolor(Pastel2) ndocolor(gs8 ..) name(base, replace) ndlab("Available districts") title({bf:Logistically unfeasible districts}) label(data("$training_data/4_Data visualization/Map/BGD_label_coor.dta") label(NAME_2) xcoord(_X) ycoord(_Y) length(20) size(*0.5) gap(*1) color(black)) legend(pos(7))<br>

graph export "$training_output/Bangladesh_map.png", as(png) replace
```
## How to create graphs with error bar? 

```stata
* 1.8.1 Graphs with error bars
```

## Great resources to learn Stata online
There is only one way to get proficient with Stata: to have PATIENCE. Practice is fundamental to become better and better, do not get discouraged if you are not able to achieve what you want at the beginning. Stata prizes people who have patience and practice with perseverance. Hopefully this training and my source code will help you navigating the immense world for Data Cleaning, Processing and Analysis with Stata and will make the whole learning path easier and funnier! In the meantime, I leave you with some sources to learn Stata online that were extremely useful for me:

[Stata official website](https://www.stata.com/links/resources-for-learning-stata/)
[UCLA website](https://stats.idre.ucla.edu/stata/)
[Princeton Stata tutorial](http://www.princeton.edu/~otorres/Stata/)
[Stata web books from UCLA](https://stats.idre.ucla.edu/stata/webbooks/)
