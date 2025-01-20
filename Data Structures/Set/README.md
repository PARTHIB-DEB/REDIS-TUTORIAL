# REDIS SETS
SET - A data structure which holds _**unordered** collections of **unique** elements_. Sets in redis follows the same rule. It is used for searching distinct elements from a sequence with single frequency. Like in maths , we can do several operations on redis sets (e.g: union , intersection etc).

In redis , sets are also mapped to a key and we do operate on the key to manipulate the values of the set

# Usecases
<img width="335" alt="{B8843B32-FF09-48D1-A6FE-A02C3D7DBE4C}" src="https://github.com/user-attachments/assets/adcce939-aaab-4725-b816-dbf171a5cf04" />

# Commmands

  - ## SADD
    To add elements in a SET , we use SADD . Now if we want to add a single element more than once , we will get response which denotes the pre-existance of the element in the set
    
    ```bash
       127.0.0.1:6379> SADD myset name
       (integer) 1
       127.0.0.1:6379> SADD myset 1010
       (integer) 1
       127.0.0.1:6379> SADD myset 1010
       (integer) 0
       127.0.0.1:6379> SADD myset true
       (integer) 1
    ```
  - ## SCARD
    To get the cardinality of a set , we use SCARD .

    ```bash
       127.0.0.1:6379> SCARD myset
       (integer) 3
    ```
  - ## SISMEMBER
    To check if an object is a member of a set

    ```bash
       127.0.0.1:6379> SISMEMBER myset 1010
       (integer) 1
    ```
    
  - ## SINTER
    To get the values that come under intersection of 2 or more sets

    _❗❗If you are giving only one set as an argument with SINTER . It will give the insected values between given set and NULL SET . As NULL SET has no values , so the intersected values = values of the given set . So technically , SINTER in this format , tells the members of a set . But , don't worry ! , there is a proper way for it. (I hope you know basic set theory) 😃_

    ```bash

       # 1st Usage (Count the members)
    
       127.0.0.1:6379> SINTER myset
       1) "name"
       2) "1010"
       3) "true"

        # 2nd Usage (Actual usage)

        127.0.0.1:6379> SADD newset parthib pink 10 X10k? 1@4^ name 1010
        (integer) 5
        127.0.0.1:6379> SINTER newset myset
        1) "name"
        2) "1010"
    ```
    
  - ## SDIFF
    Returns elements of prior set which is not in later one

    ```bash
       127.0.0.1:6379> SDIFF myset newset   # elements which are in **myset but not in newset**
       1) "1010"
       2) "true"
    ```

  - ## SINTERSTORE
    This command is equal to SINTER, but instead of returning the resulting set, it is stored in destination. If destination already exists, it is overwritten.

    ```bash
       127.0.0.1:6379> SADD key1 a 123 #$
       (integer) 3
       127.0.0.1:6379> SMEMBERS key1
       1) "a"
       2) "123"
       3) "#$"
       127.0.0.1:6379> SADD key2 ABCDE 12#%*
       (integer) 2
       127.0.0.1:6379> SINTERSTORE key key1 key2
       (integer) 0
       127.0.0.1:6379> SADD key1 ABCDE
       (integer) 1
       127.0.0.1:6379> SINTERSTORE key key1 key2
       (integer) 1
        127.0.0.1:6379> SMEMBERS key1
        1) "a"
        2) "123"
        3) "#$"
        4) "ABCDE"
        127.0.0.1:6379> SMEMBERS key2
        1) "ABCDE"
        2) "12#%*"
    ```

  - ## SRANDMEMBER
    Randomly returns X no of members of a set (X is a numerical argument)
    
    ```bash
       127.0.0.1:6379> SRANDMEMBER newset 2
       1) "10"
       2) "1@4^"
       127.0.0.1:6379> SRANDMEMBER newset 2
       1) "10"
       2) "1@4^"
       127.0.0.1:6379> SRANDMEMBER newset 2
       1) "pink"
       2) "X10k?"
       127.0.0.1:6379> SRANDMEMBER newset 2
       1) "10"
       2) "X10k?"
    ```
    
  - ## SREM & SPOP
    Both commands use to delete elements from a set. The difference is **SREM takes the name of element . SPOP takes the name of the set and the number of elements (not necessary) to pop FROM LEFT**

    ```bash
      127.0.0.1:6379> SREM myset name
      (integer) 1
      127.0.0.1:6379> SPOP newset
      "parthib"
      127.0.0.1:6379> SREM myset 1010 true
      (integer) 2
      127.0.0.1:6379> SREM myset 1
      (integer) 0
    ```

💡For more commands , explore at here ➡️ [link](https://redis.io/docs/latest/commands/?group=set)


    

