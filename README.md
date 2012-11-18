phing-joomla-extension-builder
==============================

Phing script to automate Joomla extensions building


Introduction
==============================

This script is intended to be used if you are in a situation where you develop your extensions inside a joomla tree but store them in a repository or folder outside the tree. The script provides functionality to copy the extension by name out of the joomla tree.

Naming conventions
==============================

The script uses the extension prefix to determine the extension type, so you have to use the following prefixes to the extension=VALUE

component : "com_"
module : "mod_"
template : "tpl_"
plugin: "plg_GROUP_"

Administrator modules and templates must use the following prefixes

module: "mod_admin_"
template: "tpl_admin_"

Language files
==============================

When using this script, the language files for an extension needs to be stored within the folder of the extension itself and not in the global language folder.

Usage examples
==============================

Building an extension from the joomla source tree

	phing -Dextension=com_content build

Creating a package

	Once you have built an extension you can create an installable package from the build using the following command.

	phing -Dextension=com_content

	This will create a package file "com_content_DATE.zip"

	If you also wish to add a version number you can use the following procedure

	phing -Dextension=com_content -Dversion=2.5
	
### Original source code from
https://github.com/rvsjoen/joomla-helloworld/tree/master/25
