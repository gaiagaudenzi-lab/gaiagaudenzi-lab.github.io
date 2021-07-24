---
layout: default_subpages
title: "Stata Training"
---
# Table of contents
* [Stata Basics](#stata_basics)
* [Stata Course](#stata_course)
	* [Setup](#setup)



# Stata training

This "Stata guide" is intended to be a handy resource for you, and you can use it the way you want. It is divided in topic but it is not consequential, meaning you can jump from one chapter to another without any problems. 

If you already have a knowledge of what Stata is, you can definitely skip the Stata basic part. I will try to cover from the very basic to the very advanced (as far as I know), but if you think I took something for granted, or something is not well explained shoot me a message! Feel free to copy and paste my code and send me an email at gaiagaudenzi9@gmail.com if you have problems working with the code! 


# <a name="stata_basics">Stata Basics</a>

## What is Stata? 
Nothing else than a statistic software to analyze your data! It is widely used (at least in Economics, which is the field where I come from) and it is very simple to use. You can browse through this training to have a sense of what you can do with it and get used to the language and terminology. Luckily enough, Stata has excellent official resources to learn it and great online support. If you have a question on how to do something, you can look for an answer (if it's there already) or ask your question on the forum <span style="font-size:20px">[Statalist](https://www.statalist.org/)</span>.

Here is an example of a Stata interface:

![Stata_interface]({{site.url}}/images/Stata1.png)


* <span style="color:blue;font-size:17px">History window</span>: Commands you write directly on the command prompt get stored there, so that if you want to re-run them, you just click on them and they appear on the command prompt without the need for you to type them again.
* <span style="color:fuchsia;font-size:17px">Results window</span>: Where the output from your commands, error messages and all the other programme operations get printed. You can scroll it to see what is the output of the code you wrote (regression output etc.)
* <span style="color:green;font-size:17px">Command prompt</span>: Where you can type your command (not recommended)
* <span style="color:red;font-size:17px">Variables window</span>: Where you can see all the variables and labels of the dataset that is loaded
* <span style="color:orange;font-size:17px">Properties window</span>: Where you can see all the properties of the variables of the dataset that is loaded

You should use the interface only to look at variables, at the output etc. you should NOT type from the command prompt, except for quick checks. It is extremely inefficient to type your commands directly into the Command prompt. You should use *dofiles* instead! (We'll talk about them in a second).

As it may be clear by now, Stata works with commands. Every line of code you type on Stata corresponds to a command. So with every line, you are asking Stata to perform a different action. This is an example of two lines of command in Stata:

```stata
1. use "/Users/gaiagaudenzi/Documents/Stata/dataset.dta"
2. browse
```
"translated" in plain English, these two lines of code correspond to:

<span style="font-size:20px">1. Open the dataset named "dataset.dta" that is on my laptop, specifically in the directory "/Users/gaiagaudenzi/Documents/Stata/"</span><br>
<span style="font-size:20px">2. Browse through the variables that are inside this dataset</span>

There are of course many many commands, depending on the operations you want to perform and on which variable. If you are not sure about which command you want to use, or how a command is supposed to be used, Stata will always help you. You just have to type

```stata
help
```
followed by the name of the command (Fun fact: help is itslf a command, that helps you understand other commands). Stata will open the documentation and show you some examples on how to use that command. Througout this training, I will make extensive use of the data documentation, so that you can get familiar with it and become more and more independent.

## Structure of a command

To let you know how the help command works, and what is the basic structure of a command as you see it on the Stata documentation. I take the code <code>summarize</code> as an example. It is a code that calculates for you the number of observations, the mean, the standard deviation, the minimum and the maximum of a variable. By typing <code>help summarize</code> we get the syntax of this code:

```stata
summarize [varlist] [if] [in] [weight] [, options]
```
## Stata basics 

Let’s start talking about how you can actually load datasets on Stata. The extension stata uses for its file is .dta, so the name of a dataset in Stata format will look like this: dataset.dta. However, you can import a wide variety of files with different formats into Stata (Excel, csv etc.)

## Loading data and directories

How can you locate on your laptop the files you will load into Stata? With the directory of the file itself! For every file you import/load in Stata you have to specify the directory, to tell Stata where exactly it has to find the file. So, to load a *.dta* file into Stata, you will use the following syntax:

```stata
use "yourdirectory/dataset.dta"
```

Where "yourdirectory" is the directory where the file is. For example, in the box below, I show the directory of the file example.dta contained on my computer in the directory "/Users/gaiagaudenzi/Documents/Stata"

```stata
use "/Users/gaiagaudenzi/Documents/Stata/dataset.dta"
```

This will open the file dataset.dta on Stata.

To know in which directory you are at the moment, type on the Command prompt:

```stata
pwd
```

It will return the directory Stata is in. In my case now it is:
```stata
"/Users/gaiagaudenzi/Documents/Stata/dataset.dta"
```

To change directory (in this example I change from “/Users/gaiagaudenzi/Documents/Stata” to “/Users/gaiagaudenzi/Documents/Datasets”

```stata
cd “/Users/gaiagaudenzi/Documents/Datasets”
```

To create directories (this will create folders into your laptop! In this example I create the folder “NewDirectory”)

```stata
mkdir “/Users/gaiagaudenzi/Documents/NewDirectory”
```
# Stata course

# Setup
## How to organize your workflow

### Use dofiles! 
When using Stata for research, one of your first concerns should be how to make sure your research is reproducible, and how to make sure that, if you look at a clean dataset 5 years after, you are able to trace back any modification you make to the raw data and (ideally) also know why you made that modification. Dofiles help doing all of this! Why are they called Dofiles? because their extension is  .do. Dofiles allow you to quickly reproduce your work and leave comments between your lines of code, so that you can note down what you are doing, and why you are doing it. Ideally a Dofile should be written in a way that allows another Stata user (or your future self, which 99% of the time will NOT remember why you did what you did) to understand everything you did in there without effort. 

### Create a folder structure 
You should create a folder structure on your laptop where you store all the document and data of the project so that you immediately know where they are. This is important so that you don't waste time in the future looking for "that dataset I created a wile ago".
The minimum structure I suggest is presented below:
* **Data** _here you store all the data you need for your analysis_
  * **Raw** _here you store all the raw data (not processed, saved as they come in from the server)_
  * **Processed** _here you store all the data you manipulated (partial datasets etc.)_
  * **Final** _here you store all the FINAL data (this should be the final version of the data ready for publication)_
* **Codes and documentation** _here you store all your dofiles, R script, documentation of the datasets etc._
* **Output** _here you store all your dofiles, R script etc._
  * **Tables** _here you store all the tables that come out as an output from your codes_
  * **Graphs** _here you store all the graphs that come out as an output from your codes_

*N.B. You may want to check iefolder, a user-written command the World Bank created to automatically create a folder structure from Stata.*


### Create a workflow

### Create a setting for collaborative coding
Being organized is important if you are working on a project on your own. It is much more important so when you are working with other people. Your team most likely will store the project files (Data, codes etc.) on a cloud system (Dropbox, OneDrive, GoogleDrive etc.). Every member of the team should be able to run the scripts from their personal laptop, this means Stata would need to access the data and output folder to reproduce the results. There is a very simple way to achieve this in Stata, to see it let's take a step back and explore what are macros in Stata.

### Macro (globals and locals)

A common definition for macros is the following[^1]
> Macros are abbreviations for a string of characters or a number. 

It might not seem so at the moment, but macros are very powerful tools we will use throughout this course. The two macros we will describe now are `local` and `global`. 

First of all, let's see which description Stata offers for them:

>global assigns strings to specified global macro names (mnames). local assigns strings to local macro names (lclnames). Both double quotes (" and ") and compound double quotes (‘" and "’) are allowed

This might look very obscure to you, but I promise it will be clear in a moment. 

At this stage I would like to think about macros an empty box, where you can store content. You can store pretty much anything you want in that box, either numbers or letters.

`local` are macros that are valid only as long as you execute commands in do-files.  
`globals` are macros that are valid for the entire duration of the Stata session (so they are valid until you cancel them or you close Stata). A Stata session lasts from the moment you open Stata to the moment you close it. Meaning if you load another dataset without having closed Stata previously, you are in the same Stata session.

Let's look at the syntax for local

`local localname "string"`   _This allows you to store strings_  
`local localname = expression` _This allows you to store numbers_

#### Example 1: Create your first local
I want to create a local that stores my name, so that when I "call" it or execute it, it will return my name:

``` code
local my_name "Gaia Gaudenzi"
display "`my_name'"
```
Try to copy this code in a dofile, replace it with your name and run the code. What happens? What happens if you run the lines separately?

#### Example 2: Create your first global
Similarly as we did before, I will create a global that stores my cat name (Minou), so that when I "call" it or execute it, it will return my cat's name:

``` code
global my_cat_name "Minou"
display "$my_cat_name"
```
Try to copy this code in a dofile, replace it with your name and run the code. What happens? What happens if you run the lines separately?

**Ok. great. But how is this useful?** Since globals store strings, we can use them to store directories so that we don't have to type always the entire directory of a file when we import/export it. This reduces errors and forces you to organize files in "bins" that can be accessed through pre defined globals.

#### Application 1: Create your first global that stores directory

Let's say I have a Data folder where I store all my data, and I want to import an Excel (called SampleExcel.xlsx) from that folder. The directory of that folder on my laptop is  
"/Users/gaiagaudenzi/Documents/Stata/Data"
> Note that this directory is specific to my laptop, i.e. it specifically indicates the location of the Data folder on my laptop.

If I want to import SampleExcel.xlsx into Stata, I would have to write:

``` code
import excel using "/Users/gaiagaudenzi/Documents/Stata/Data/SampleExcel.xlsx"
```

# Data cleaning
## Explore your data

### destring/tostring
 ```code
    rename _all, lower 
    destring(var), replace
    tostring(var), replace 
```

### Identify missing values 
 ```code
mvdecode _all, mv(99=.m \ 96=.d )
```

## Renaming variables
## Labeling variables
## Cleaning strings
### Extended functions
## Working with dates

# Data processing
## Data manipulation
## Randomization
## Automation: Loops

# Data exporting

# Data analysis

# Data visualization
Did you know you can create simple maps in Stata? This is thanks to the absolutely awesome people that invented the spmap command. 
```stata
* 1.8.2 Maps

* 1 STEP: Convert shapefile to .dta

	shp2dta using "$training_data/4_Data visualization/Map/gadm36_BGD_2.shp", data("$training_data/4_Data visualization/Map/BGD_zilamap") coor("$training_data/4_Data visualization/Map/BGD_zilacoor") replace genid(id)
	
	u "$training_data/4_Data visualization/Map/BGD_zilamap.dta", clear
	
	spmap using "$training_data/4_Data visualization/Map/BGD_zilacoor.dta" , id(id) 

* Mark unfeasible districts

	u "$training_data/4_Data visualization/Map/BGD_zilamap.dta", clear

	* 1.1 Mark Hill tract areas
	#delim ;
	g var = "Hill tract/Cox's"
	if NAME_2 == "Chittagong" 
	| NAME_2 == "Khagrachhari" 
	| NAME_2 == "Rangamati"
	| NAME_2 == "Bandarban" 
	| NAME_2 == "Cox'S Bazar"
	;
	#delim cr

	* 1.2 Mark Haor areas
	#delim ;
	replace var = "Haor areas" 
	if NAME_2 == "Sylhet" 
	| NAME_2 == "Maulvibazar"
	| NAME_2 == "Habiganj"
	| NAME_2 == "Sunamganj"
	;
	#delim cr

	* 1.3 Mark areas affected by Cyclones
	#delim ;
	replace var = "Cyclones" 
	if NAME_2 == "Khulna"
	| NAME_2 == "Bagerhat" 
	| NAME_2 == "Pirojpur" 
	| NAME_2 == "Jhalokati"
	| NAME_2 == "Patuakhali"
	| NAME_2 == "Barguna"
	| NAME_2 == "Bhola"
	| NAME_2 == "Noakhali" 
	| NAME_2 == "Satkhira"  
	;
	#delim cr

	* 1.4 Mark areas affected by flooding
	#delim ;
	replace var = "Flooding" 
	if NAME_2 == "Faridpur" 
	| NAME_2 == "Sirajganj" 
	| NAME_2 == "Tangail"
	| NAME_2 == "Jamalpur" 
	| NAME_2 == "Gaibandha" 
	| NAME_2 == "Lakshmipur" 
	;
	#delim cr

	* 1.5 Mark areas affected by water logging
	replace var = "Water Logging" if NAME_2 == "Jessore" 

	* 1.6 Mark areas affected by flash flood (if not already eliminated)
	replace var = "Flash flood" if NAME_2 == "Netrakona" 

	encode var, g(var2)
	
	preserve
	* Create labels (not compulsory)
	u "$training_data/4_Data visualization/Map/BGD_zilacoor.dta", clear
	collapse (mean) _X _Y, by(_ID)
	rename _ID id
	merge 1:1 id using "$training_data/4_Data visualization/Map/BGD_zilamap.dta"
	keep id _X _Y NAME_2
	save "$training_data/4_Data visualization/Map/BGD_label_coor", replace
	restore
	
	* 1.7 Create map
	spmap var2 using "$training_data/4_Data visualization/Map/BGD_zilacoor.dta" , id(id) clmethod(unique)  ocolor(gs8 ..) fcolor(Pastel2) ndocolor(gs8 ..) name(base, replace) ndlab("Available districts") title({bf:Logistically unfeasible districts}) label(data("$training_data/4_Data visualization/Map/BGD_label_coor.dta") label(NAME_2) xcoord(_X) ycoord(_Y) length(20) size(*0.5) gap(*1) color(black)) legend(pos(7))

graph export "$training_output/Bangladesh_map.png", as(png) replace
```
## How to create graphs with error bar? 

```stata
* 1.8.1 Graphs with error bars
```

# Great resources to learn Stata online
There is only one way to get proficient with Stata: to have PATIENCE. Practice is fundamental to become better and better, do not get discouraged if you are not able to achieve what you want at the beginning. Stata prizes people who have patience and practice with perseverance. Hopefully this training and my source code will help you navigating the immense world for Data Cleaning, Processing and Analysis with Stata and will make the whole learning path easier and funnier! In the meantime, I leave you with some sources to learn Stata online that were extremely useful for me:

* <span style="font-size:20px">[Stata official website](https://www.stata.com/links/resources-for-learning-stata/){:target="_blank"}</span>
* <span style="font-size:20px">[UCLA website](https://stats.idre.ucla.edu/stata/){:target="_blank"}</span>
* <span style="font-size:20px">[Princeton Stata tutorial](http://www.princeton.edu/~otorres/Stata/){:target="_blank"}</span>
* <span style="font-size:20px">[Stata web books from UCLA](https://stats.idre.ucla.edu/stata/webbooks/){:target="_blank"}</span> 
* <span style="font-size:20px">[Code and Data](https://web.stanford.edu/~gentzkow/research/CodeAndData.pdf){:target="_blank"}</span>
* <span style="font-size:20px">[Getting Started in Data Analysis using Stata](https://www.princeton.edu/~otorres/StataTutorial.pdf){:target="_blank"}</span>
* <span style="font-size:20px">[Stata Tutorial](https://econweb.ucsd.edu/~elib/120b/Stata%20Tutorial.pdf){:target="_blank"}</span>
* <span style="font-size:20px">[Stata Basic](https://edge.edx.org/assets/courseware/v1/85458a6abe1e09fb891fb8f8610dffbd/c4x/BerkeleyX/CEGA101AIE/asset/Module_1.2_STATA_Basics.pdf){:target="_blank"}</span>
* <span style="font-size:20px">[Getting Started with Stata, Princeton University](http://www.princeton.edu/~otorres/Stata/){:target="_blank"}</span>

# References

[^1]: Long, J. Scott. 2009. The Workflow of Data Analysis Using
Stata. College Station, TX: Stata Press.
