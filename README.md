# PowerQuery Complex Algorithm

Supposed you need to build a project dimension table from an API call that will return a JSON file with a projects’ hierarchy. Each level could represent an organization structure like Division/Department/Project or something similar. How to load this kind of structure with PowerQuery when you don’t know how deep is the structure.
If you try to do it with the Power BI Desktop wizard and menus, it will probably be hard-coded for a fix number of levels and it will be difficult to maintain.
The PowerQuery language (the M language) is very powerful and we can code very complex algorithm with it. As this language is more a functional language, it’s not easy to figure out how to do it. By example it’s very easy to code that with Python, but with PowerQuery you must look deep on all features available by the language to find out a way to do it.
  
## The json file structure
![GitHub Logo](/json.png)
  
## The result
![GitHub Logo](/result.png)  
   
## The source code
![GitHub Logo](/code.png) 
  
## see raw_code.txt and projects.json for the source json file and the code that you can use with PowerBI Desktop
  
