# servicenow-data
Bit of script to make the GlideRecord stuff reusable.

There is a dependency on underscore, which I have provided here as well, if you don't have loaded in your instance already. If you already have underscore loaded, make sure that the name of the script include is literally "_", otherwise it won't work in the server scripts of Service Portal widgets.

#### Usage:
  * get(): Use this to query a table
            
            Data.get({"tableName": "incident", "query": "short_description=some description", "page": 1, "recordsPerPage": 5}})           
            
  * set(): Use this to perform insert, updated, delete and merge (update or insert) operations
             
             INSERT: Data.set({"tableName": "incident", "insert": {"short_description": "insert this"}})
             UPDATE: Data.set({"tableName": "incident", "query": "short_description=match this", "update": {"short_description": "update this"}})
             MERGE: Data.set({"tableName": "incident", "query": "short_description=match this", "merge": {"short_description": "insert or update this"}})
             DELETE: Data.set({"tableName": "incident", "delete": "short_description=match this"}})

#### Options:
  When invoking "get", there are the following options available:
  
  * **recordsPerPage (integer)**: The number of records to show per page. When this option is supplied, it will turn on pagination.
  * **page (integer)**: Which page to show. This requires *recordsPerPage* to be supplied as well.
  * **isComplex (boolean)**: If this is true, it will return a complex object for each field in the following format:
  
      ```
      
      {
        "value": "sample display value",
        "displayValue": "Sample Display Value",
        "label": "Field name",
        "table": "table name"
      }
                
      ```
  			
  
  * **orderBy (string)**: Which field to order by. Needs to be in the format `<field_name> <direction>` (if no direction is supplied, default is DESC).
  
    For example:
    
    ```
    number ASC
    ```
    
    ```
    short_description DESC
    ```
  * **fields (csv string, or array of strings)**: The columns you want to return. If not supplied, all the columns will be returned. This takes a csv string, or a list of strings.