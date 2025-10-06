
templetes  --> we can keep some placeholders, you can put the values at run time

file --> content inside a specific file

# ansible templates #
follows jinja2 formatting, we can keep some placeholders, actual values will be be provided through variables at runtime 

ansible templates
=================
follows jinja2 formatting, we can keep some placeholders, actual values will be provided through variables at runtime.

tasks
	main.yaml --> playbook related tasks are her
files
	<file-name> --> you can keep all the files required here
templates
	<template-file> --> we can keep all the templates with placeholders here. usually we follow jinja2 templating, variables values can be supplied
vars
	main.yaml --> all variables required for roles can be kept here.
    
handlers --> handlers are notifiers in ansible. when there is a change in something if you want to notify other task we can use handlers. for example change in nginx configure can notify restart nginx task in handlers
	main.yaml