# phing-joomla-extension-builder

Phing script for Joomla 2.5 and 3.0 extension building automation.

## Introduction

If you are developing an extension or template inside a Joomla site, and you need to fetch all the changes and create an new installer for that specific extension, this script is the solution to do this job automatically.

## Considerations

To use this script your extension and templates files and folders must follow the Joomla standard naming conventions and typical folder structures for extension and templates.

The following example shows how a component folders and files looks before and after the installation, to figure out how other extension move the files and folder before and after the installation consult the XML manifest file of the given extension.

(!) Note that the language files must be inside the component folder for "administrator" side and "site" side, this is the new standard for 1.6+ Joomla sites

**Before installation**

	com_mytestcomponent
	├── admin
	│   ├── controller.php
	│   ├── controllers
	│   ├── mytestcomponent.php
	│   ├── index.html
	│   ├── language (!)
	│   ├── models
	│   ├── sql
	│   ├── tables
	│   └── views
	├── mytestcomponent.xml  (manifest file)
	├── media
	│   ├── css
	│   ├── images
	│   └── js
	└── site
	    ├── controller.php
	    ├── controllers
	    ├── mytestcomponent.php
	    ├── index.html
	    ├── language (!)
	    ├── models
	    ├── router.php
	    └── views

**After installation**

	mytestjoomlasite
	├── administrator
	│   └── components
	│       └── com_mytestcomponent
	│           ├── controller.php
	│           ├── controllers
	│           ├── mytestcomponent.php
	│           ├── index.html
	│           ├── language
	│           ├── models
	│           ├── sql
	│           ├── tables
	│           ├── views
	│           └── mytestcomponent.xml  (manifest file)
	├── components
	│   └── com_mytestcomponent
	│       ├── controller.php
	│       ├── controllers
	│       ├── mytestcomponent.php
	│       ├── index.html
	│       ├── language
	│       ├── models
	│       ├── router.php
	│       └── views
	└── media
	    └── com_mytestcomponent
	        ├── css
	        ├── images
	        └── js

## Instructions

For this instructions we will assume the following example setup

- The Joomla site is located at

	/home/youruser/lamp/public_html/mytestjoomlasite/
	
- The extension source folder is located at

	/home/youruser/Documents/mytestcomponent/

This is a typical Linux folder structure replace "/home/youruser/" with "C:\Users\username" for Winblow$ machines.

### Script files

Get inside your extension source folder

	/home/youruser/Documents/mytestcomponent/

Inside this folder copy and paste the following script files

- build.xml
- build.properties.dist

Open the file

	build.properties.dist
	
The parameter "source.dir" sets the location of your Joomla site, this should looks like this

	source.dir=/home/youruser/lamp/public_html/mytestjoomlasite/

Save changes

### Building an extension

Assuming you already have your component "mytestcomponent" installed in your "mytestjoomlasite" Joomla site, then let's proceed to build a new installer with that information.

The script uses the extension prefix to determine the extension type, so you have to use the following prefixes:

- component : "com_"
- module : "mod_"
- template : "tpl_"
- plugin: "plg_GROUP_"

Administrator modules and templates must use the following prefixes:

- module: "mod_admin_"
- template: "tpl_admin_"

In our case we are working with a normal component so our prefix will be "com_"

Open your terminal and locate at the extension source folder folder

	cd /home/youruser/Documents/mytestcomponent/

Now to build the extension run the following command

	phing -Dextension=com_mytestcomponent build

If no error messages are present, then congratulations you just build your first component installer "+1 for you"

To create a build with a custom version number use 

	phing -Dextension=com_mytestcomponent build -Dversion=x.x.x

Where "x.x.x" are the version numbers, for example "1.0.2"


#### Warning

To build the extension this script **deletes** the content of the extension source folder and then copy the extension files from the Joomla site, in other words, don't make changes on the files and folders of your extension source location because the can be delete by the script, instead do the changes in the Joomla site and build the extension again.

## More Examples

### Building extension from the Joomla site

We can build any installed extension from the Joomla site, for example, we can build the component "com_content" whit is responsible to manage and display articles.

	phing -Dextension=com_content build

Note: This example assumes you have already have a source folder for this extension and have the script parameters configured correctly

### Creating a package

Once you have built any extension you can create an installable package from the build using the following command.

	phing -Dextension=com_mytestcomponent

This will create a package file "com_mytestcomponent_DATE.zip"

If you also wish to add a version number you can use the following procedure

	phing -Dextension=com_mytestcomponent -Dversion=2.5

or

	phing -Dextension=com_mytestcomponent -Dversion=3.0

### Using an alternative name for the build file

If for some reason you need to rename the file "build.xml" use this parameter to tell phing to run your custom named build file "-f <filename>", i.e.: Let's say we renamed our build file from "build.xml" to "phing-joomla-extension-builder.xml", the execution command will looks like this. 

	phing -Dextension=com_mytestcomponent build -f phing-joomla-extension-builder.xml

## Original source code and idea from

https://github.com/rvsjoen/joomla-helloworld/tree/master/25

