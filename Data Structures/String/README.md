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

