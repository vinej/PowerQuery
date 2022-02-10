## PowerQuery Complex Algorith

Supposed you need to build a project dimension table from a API call that will return a json file with a hierarchy of projects. Each level could represent an organisation structure like <Division>/<Departement>/<Project> or something similar. How to load this kind of structure with PowerQuery when you don’t know how deep is the structure.
If you try to do it with the PowerBI Desktop wizard and menus, it will be probably hardcoded for a fix number of levels and it will be difficult to maintain.
The PowerQuery language (the M language), is very powerfull and we can code very complex algorithm with it. As the M language is more a functional language, it’s not easy to figure out how to do it. By example it’s very easy to code that with Python, but with PowerQuery you must look deep on all features available by the langage to find out a way to do it.
  
# The json file structure
![GitHub Logo](/json.png)
  
# The result
![GitHub Logo](/result.png)  
   
# The source code
![GitHub Logo](/code.png) 
  
