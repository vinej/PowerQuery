## PowerQuery Complex Algorith

Supposed you need to build a project dimension table from an API call that will return a JSON file with a projects’ hierarchy. Each level could represent an organization structure like <Division>/<Department>/<Project> or something similar. How to load this kind of structure with PowerQuery when you don’t know how deep is the structure.
If you try to do it with the Power BI Desktop wizard and menus, it will probably be hard-coded for a fix number of levels and it will be difficult to maintain.
The PowerQuery language (the M language) is very powerful and we can code very complex algorithm with it. As this language is more a functional language, it’s not easy to figure out how to do it. By example it’s very easy to code that with Python, but with PowerQuery you must look deep on all features available by the language to find out a way to do it.
  
# The json file structure
![GitHub Logo](/json.png)
  
# The result
![GitHub Logo](/result.png)  
   
# The source code
![GitHub Logo](/code.png) 
  
# Raw code (no color)
 let
    /* read the json file, in real life a call to a REST service return json */
    Source = Json.Document(File.Contents("C:\test\v2.5\pr.json")),
    /* create a empty table */
    emptytable = #table( columns, {} ),
    /* create the list of columns to manage from the json file */
    columns = { "name", "level", "path", "children"},
    /* get the root record and create the root table with it. The MissingFiled.UseNull parameter is important */
    /* because the field <children> won't be there if the record has no children */
    root = Table.FromRecords( { (Source) }, columns,  MissingField.UseNull ),
    /* recursive function that will be call with a list of records */
    get = (childs) => let
      /* here the <childs> variable is a LIST of records that is never null */
      /* so we create a temp table from that list for the columns we want */
      tbl = Table.FromRecords(childs, columns, MissingField.UseNull),
      /* the goal here is to call the get function of each record with the children's list */
      all = Table.Combine( 
                  /* we need to combine the list of tables created from the get function */
                  List.Combine( 
                    { 
                      /* we combine the tbl from the current recursion */
                      { tbl }, 
                      /* we will call recursively the get function with each children of the current record for the list <childs> */
                      /* List.Transform, will call many time the get function for each record of the list */
                      /* so we generate tmp table, and we will combine all of them into one table : all */
                      List.Transform( childs, (c) => if c[children]? = null then emptytable else @get(c[children]?)) 
                    }
                  )
            )
    in
      all,
    /* call the get function with the root children */
    alltables = get(Source[children]),
    /* combine the root with all tables returned from the get function */
    roorall = Table.Combine( { root, alltables } ),
    /* add a column "is_leaf" to distinquid level considered as parent and the lowest levels that contain record with no children */
    addisleaf = Table.AddColumn(roorall, "is_leaf", each if [children] = null then 1 else 0),
    /* remove the column "children" that contain null is not children or a list if there were children */
    removechildrencolumn = Table.RemoveColumns(addisleaf, { "children"})
in
    removechildrencolumn
  
