# PowerQuery Complex Algorithm

## (1) How to read a json hierarchy with PowerQuery

Supposed you need to build a project dimension table from an API call that will return a JSON file with a projects’ hierarchy. Each level could represent an organization structure like Division/Department/Project or something similar. How to load this kind of structure with PowerQuery when you don’t know how deep is the structure.
If you try to do it with the Power BI Desktop wizard and menus, it will probably be hard-coded for a fix number of levels and it will be difficult to maintain.
The PowerQuery language (the M language) is very powerful and we can code very complex algorithms with it. As this language is more a functional language, it’s not easy to figure out how to do it. By example it’s very easy to code that with Python, but with PowerQuery you must look deeper on all features available by the language to find out a way to do it.

See below how to do it. I used this kind of algotithm in a real life scenario to build dimensions and facts tables from API calls and it worked very well.
  
### The json file structure
![GitHub Logo](/json.png)
  
### The result
![GitHub Logo](/result.png)  
   
### The source code
![GitHub Logo](/code.png)

## (2) Transform a path field into columns

Supposed with the previous result, we want to create dynamic columns for all parts of the path field. We want the result below

### The result we want
![GitHub Logo](/result2.png)

### The source code
![GitHub Logo](/code2.png)

## (3) Recreate the organisation structure Sector/Bu/Division/Project

Supposed the client gave more complex specifications. 
- He wants only the last level (is_leaf=1)
- He said that 4 levels represent the organisation hierarchy with 4 minimum levels Sector/Bu/Division/Project
- It could have more levels 
- the sector level does always start at the same level. It's not standard. 
- He wants only records from a list of know sectors.

### The result we want
![GitHub Logo](/result3.png)

### The code
![GitHub Logo](/code3a.png)
![GitHub Logo](/code3b.png)

JYV
