# *SLQL*
SLQL - string lightweight query language (partially based on SQL standarts)

Linked: 

SLDB - https://github.com/ZikkeyLS/SLDB

FastSLQL - https://github.com/ZikkeyLS/FastSLQL

### TIL – Table Interaction Language
* **CREATE** - create table;
* **EDIT** - edit table;
* **DELETE** - remove table;
### EVL – Element View Language
* **GET** – get element;
* **INSERT** – add element;
* **CHANGE** – change element;
* **REMOVE** – remove element;

## Description
### TIL

* **CREATE** 

  **Arguments:**
  
    CREATE [*TABLE_NAME*] [*arguments*(unrequired)]
  
  **Examples:**
  
    ```
    CREATE TEST (user_token(U) | user_name(U, Min(4), Max(16)) | user_password(Min(6), Max(20)))
    ```
    
* **EDIT**

  **Arguments:**
  
    EDIT STRUCTURE [*TABLE_NAME*] [*value*]
  
    EDIT NAME [*TABLE_NAME*] [*NEW_TABLE_NAME*]
  
  **Examples:**
    ```
    EDIT TEST NAME TEST1
    
    EDIT TEST1 STRUCTURE (user_token(U) | user_name(U, Min(4), Max(16)) | user_password(Min(6), Max(20)) | user_status)
    ```
    
  **Parametres:**
    ```
    U - unique. Means that only one element can be in table with a unique value.
  
    Min(x) - minimum amount of symbols
  
    Max(y) - maximum amount of symbols
    ```

* **DELETE**

  **Arguments:**
  
    DELETE [*TABLE_NAME*]  
    
  **Examples:**
    ```
    DELETE TEST
    ```
      
### EVL

* **GET** 

  **Arguments:**
  
    GET [*TABLE_NAME*] [*id*]
    
    GET [*TABLE_NAME*] [*ALL / First {index} / Last {index}*] (where [*name1*]=[*value1*] ( [*name2*]=[*value2*] **etc...**)(unrequired))
    
    GET [*TABLE_NAME*] LENGHT (where [*name1*]=[*value1*] (& [*name2*]=[*value2*] **etc...**)(unrequired))
  
  **Examples:**
  
    ```
    GET TEST1 10

    GET TEST2 ALL

    GET TEST3 ALL where banned="false"
    
    GET TEST3 First 10 where status="user" username="Aleksey"

    GET TEST4 LENGHT where banned="true"
    ```

* **INSERT**

  **Arguments:**
  
    INSERT [*TABLE_NAME*] [*value*]
  
  **Examples:**
  
    ```
    INSERT TEST (1 | "Test" | "0101")
    ```
    
* **CHANGE**

  **Arguments:**
  
    CHANGE [*TABLE_NAME*] [*index*] with [*value*]
    
    CHANGE [*TABLE_NAME*] parameter([*parameter_index*]) where [*parameter_index_name*]=[*some_value*] (& [*name2*]=[*value2*] **etc...**) with [*sub_value*]
    
    CHANGE [*TABLE_NAME*] where [*name1*]=[*value1*] ( [*name2*]=[*value2*] **etc...**) with [*value*]
    
  **Examples:**
  
    ```
    CHANGE Test1 1 with (user_token="1" | user_name="Test" | user_password="0101")
    
    CHANGE Test1 5 with user_token="1"
    
    CHANGE Test1 where user_name="Name" with user_name=""
    
    CHANGE Test1 where user_name="Test" with (user_token="1" | user_name="Test" | user_password="01010") 
    ```
    
* **REMOVE**

  **Arguments:**
  
    REMOVE [*TABLE_NAME*] [*index*]
    
    REMOVE [*TABLE_NAME*] where [*name1*]=[*value1*] (& [*name2*]=[*value2*] **etc...**)
    
  **Examples:**
    ```
    REMOVE Test 1
    
    REMOVE Test where user_name="Name"
    ```
