# REDIS HASHES
Hash - mapping a value to a field (not key 😉) . It differs in the line where HASH is just a DS which perfectly resembles with java hashmap , python dict and ruby dict , whereas redis' key-value pair is the only way to store data of any data-structure it follows.

Hashes in Redis , gives a little bit feeling of a db . That's why , Redis-OM uses HashModel as their data model to store data in redis.

To use Hashing , we need a hash-index which will hold the fields and values , or we can say under the hash-index , the fields will be linked to seperate values .

# Usecases
![image](https://github.com/user-attachments/assets/aa6728c0-6dc9-488f-b3b9-98d237340c73)


# Commmands

  - ## HGET & HSET
    Set some value to a Hash-Key or Field using HSET . Fetch its value using HGET 
    
    ```bash
       127.0.0.1:6379> HSET car:1 model "lamborgini" color "green" engine "XOG Bullseye" available 10  # 'car:1' is hash-index
       (integer) 4
       127.0.0.1:6379> HGET car:1 model # 'model' is key
       "lamborgini"
    ```
  - ## HGETALL
    Just fetches all hash-keys/fields and their respective values of a certain hash-index

    ```bash
       127.0.0.1:6379> HGETALL car:1
       1) "model"
       2) "lamborgini"
       3) "color"
       4) "green"
       5) "engine"
       6) "XOG Bullseye"
       7) "available"
       8) "10"
    ```
  - ## HINCRBY
    It increases the value of a certain field of a hash-index

    ```bash
       127.0.0.1:6379> HINCRBY  car:1 available 10      # increase the field - available by 10 (now its 20)
       (integer) 20
    ```
    
  - ## HDEL
    It deletes one or more than one hash-keys of a certain hash-index

    ```bash
       127.0.0.1:6379> HDEL car:1 available              # Deletes field - available 
       (integer) 1
    ```
    
  - ## HEXISTS
    To check if a field of a hash-index exists or not

    ```bash
       127.0.0.1:6379> HEXISTS car:1 model
       (integer) 1
       127.0.0.1:6379> HEXISTS car:1 available
       (integer) 0
    ```

  - ## HKEYS
    Fetches only fields or hash-keys under a hash-index

    ```bash
       127.0.0.1:6379> HKEYS car:1
       1) "model"
       2) "color"
       3) "engine"
    ```

  - ## HMGET
    Shows values of the fields passed as arguments of a certain hash-index

    ```bash
       127.0.0.1:6379> HMGET car:1 model color engine
       1) "lamborgini"
       2) "green"
       3) "XOG Bullseye"
    ```
    
  - ## HVALS
    just shows all the values of all fields of a hash-index

    ```bash
       127.0.0.1:6379> HVALS car:1
       1) "lamborgini"
       2) "green"
       3) "XOG Bullseye"
    ```

💡For more commands , explore at here ➡️ [link](https://redis.io/docs/latest/commands/?group=hash)


    

