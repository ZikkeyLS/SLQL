# *SOQL*
SOCL - string oriented query language (partially based on SQL standarts)

### TIL – Table Interaction Language
* **CREATE** - create table;
* **EDIT** - edit table;
* **REMOVE** - remove table;
### EVL – Element View Language
* **GET** – get element;
* **INSERT** – add element;
* **CHANGE** – change element;
* **DELETE** – remove element;

## Description
### TIL

* **CREATE** 

  **Arguments:**
  
    CREATE [*TABLE_NAME*] [*arguments*(unrequired)]
  
  **Examples:**
  
    ```[*TABLE_NAME*] = TEST
  
    [*new_value*] = user_token(U), user_name(U, Min(4), Max(16)), user_password(Min(6), Max(20))
  
    CREATE [*TABLE_NAME*] [*new_value*]
    ```
    
* **EDIT**

  **Arguments:**
  
    EDIT STRUCTURE [*TABLE_NAME*] [*value*]
  
    EDIT NAME [*TABLE_NAME*] [*NEW_TABLE_NAME*]
  
  **Examples:**
    ```
    [*arguments*] = user_token(U), user_name(U, Min(4), Max(16)), user_password(Min(6), Max(20), user_status))
    
    EDIT STRUCTURE TEST [*value*]
    
    -------------------------------------------
    
    EDIT NAME TEST TEST1
    ```
    
* **DELETE**

  **Arguments:**
  
    DELETE [*TABLE_NAME*]  
    
  **Examples:**
    ```
    DELETE TEST
    ```

  ### Parametres:
  
      U - unique. Means that only one element can be in table with a unique value.
  
      Min(x) - minimum amount of symbols
  
      Max(y) - maximum amount of symbols
      
### EVL

* **GET** 

  **Arguments:**
  
    GET [*TABLE_NAME*] [*id*]
    
    GET [*TABLE_NAME*] [*ALL / First {index}/Last {index} / From {index}/Without {index}*]
    
    GET [*TABLE_NAME*] [*tags*] where [*name1*]=[*value1*] (& [*name2*]=[*value2*] **etc...**)
    
    GET [*TABLE_NAME*] LENGHT (where [*name1*]=[*value1*] (& [*name2*]=[*value2*] **etc...**)(unrequired))
  
  **Examples:**
  
    ```
    [*tags*]=Last 20 From 3 Without 5
    GET TEST1 [*tags*] where age=5
    ---------------------------------------
    GET TEST2 ALL
    ---------------------------------------
    GET TEST3 ALL where banned=false
    ---------------------------------------
    GET TEST4 LENGHT where banned=true
    ```

* **INSERT**

  **Arguments:**
  
    INSERT [*TABLE_NAME*] [*value*] [*place_index*(unrequired)]
    
    INSERT [*TABLE_NAME*] [*value*] [*BEFORE/AFTER*] [FIRST/LAST/*place_index*] where [*name1*]=[*value1*] (& [*name2*]=[*value2*] **etc...**)
  
  **Examples:**
  
    ```
    [*value*] = user_token="0" user_name="Test" user_password="0101"
    INSERT TEST [*value*] 0
    ---------------------------------------
    INSERT TEST2 [*value*] AFTER FIRST where user_name="Name"
    ```
    
* **CHANGE**

  **Arguments:**
  
    CHANGE [*TABLE_NAME*] [*index*] with [*value*]
    
    CHANGE [*TABLE_NAME*] with [*value*] where [*name1*]=[*value1*] (& [*name2*]=[*value2*] **etc...**)
    
    CHANGE [*TABLE_NAME*] parameter [*parameter_index*] from [*index*] with [*sub_value*]
    
    CHANGE [*TABLE_NAME*] parameter [*parameter_index*] with [*sub_value*] where [*parameter_index_name*]=[*some_value*] (& [*name2*]=[*value2*] **etc...**)
    
  **Examples:**
  
    ```
        CHANGE Test1 0 with user_token="0" user_name="Test" user_password="0101"
        CHANGE Test1 with user_token="0" user_name="Test" user_password="01010" where user_name="Test"
        CHANGE Test1 parameter 0 from 5 with user_token="0" user_name="Test" user_password="01010"
    ```
