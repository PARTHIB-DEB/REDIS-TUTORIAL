# REDIS STRINGS
Strings are the most common datatype in Redis . Pretty much everything can be stored in a string . As we know **keys are always STRING** but values can also be of string datatype .

# Properties
 - By default, a single Redis string can be a maximum of 512 MB.
 - Operations on String vary from O(1) to O(N)

# Commmands

  - ## GET and SET
    GET and SET are basic keywords/commands used in redis . GET is used to fetch/show a key's value and SET is used to create/update a key's value and save it .
    
    ```bash
      127.0.0.1:6379> SET family:A1 Father:Samuel    # Key -> family:A1
      OK
      127.0.0.1:6379> GET family:A1      # Value -> Father:Samuel
      "Father:Samuel"
    ```
  - ## DEL
    DEL simply means DELETE , Yes its DELETES the Key with its Value.

    ```bash
      127.0.0.1:6379> DEL family
      (integer) 0
      127.0.0.1:6379> DEL family:A1
      (integer) 1
    ```
 Now before moving furthur to more commands , let's create a whole damn family 😆 in redis .

 ```bash
   127.0.0.1:6379> SET family:A1:Father samuel
   OK
   127.0.0.1:6379> GET family:A1
   (nil)
   127.0.0.1:6379> GET family:A1:Father
   "samuel"
   127.0.0.1:6379> SET family:A1:Mother Maria
   OK
   127.0.0.1:6379> GET family:A1:Mother
   "Maria"
   127.0.0.1:6379> SET family:A1:Uncle Nick nx    # Nick is not a value
   OK
   127.0.0.1:6379> GET family:A1:Uncle
   "Nick"
   127.0.0.1:6379> SET family:A1:Uncle Nick nx    # Nick is already a value
   (nil)
   127.0.0.1:6379> SET family:A1:Uncle Nick xx    # # Nick is already a value
   OK
   127.0.0.1:6379> GET family:A1:Uncle
   "Nick"
   127.0.0.1:6379> SET family:A1:Grandmother univea nx
   OK
   127.0.0.1:6379> SET family:A1:Grandmother univea xx
   OK

 ```
❗**nx** : nx is a secondary argument which tells **to set the value if it doesn't exists** , basically a **new value**
            (Or You can use **SETNX** command also , same result will happen)

❗**xx** : xx is a secondary argument which tells **to set the value if it exists**

⭐ **nx , xx** are two arguments of **SET** command

To know more about ➡️ [link](https://redis.io/docs/latest/commands/set/)

  - ## GETSET
    GETSET is a command which creates/updates a value of a key . Basically It SETs the new value and returns the old value of a key . Look at the snippet below ,
    
    ```bash
     127.0.0.1:6379> GETSET ckey 1   # No Previous key 'ckey' , so creating new and returning 'nil'
     (nil)
     127.0.0.1:6379> GET ckey
     "1"
    127.0.0.1:6379> GETSET family:A1:Uncle Damian  # Key exists , hence old value returned
     "Nick"
    ```
  - ## MSET & MGET
    MSET (Multiple SET) is used for setting multiple values to multiple keys and MGET is to fetch multiple values of multiple keys

    ```bash
     127.0.0.1:6379> MSET family:A2:Father "Joseph"  family:A3:Father "Alex"
     OK
     127.0.0.1:6379> MGET family:A2:Father family:A3:Father
     1) "Joseph"
     2) "Alex"
    ```
  - ## INCR , INCRBY , DECR , DECRYBY
    When we store any INTEGER in a STRING value and link it to a key - it is called as COUNTER value . Remember here the value must be INTEGER only . Hence we can use this commands to change the numerical value of the key
    
    ```bash
     127.0.0.1:6379> SET pkey 100
     OK
     127.0.0.1:6379> INCR pkey   # Increase by 1
     (integer) 101
     127.0.0.1:6379> INCRBY pkey 10    # Increase by custom value - 10
     (integer) 111
     127.0.0.1:6379> DECR pkey    # Decrease by 1
     (integer) 110
     127.0.0.1:6379> DECRBY pkey 9    # Decrease by custom value - 9
     (integer) 101
     127.0.0.1:6379> SET family:A1:pets 1
     OK
     127.0.0.1:6379> GET family:A1:pets
     "1"
     127.0.0.1:6379> INCR family:A1:pets
     (integer) 2
     127.0.0.1:6379> GET family:A1:pets
     "2"
    ```


