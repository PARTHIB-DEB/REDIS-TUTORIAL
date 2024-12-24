# REDIS-TUTORIAL [![My Skills](https://simpleskill.icons.workers.dev/svg?i=redis)](https://redis.io/) [![My Skills](https://skillicons.dev/icons?i=redis)](https://redis.io/)
Redis - Remote Dictionary Server . Built by Salvatore Sanfilippo (known as antirez) in 2009. **Redis Labs** (Previously knew as **Garantia Data**) , is the organisation which maintains redis.

# Major changes in 2024 💡
Maybe some of us has got a recent spiced up news of redis's sudden license change which created an internal conflict within the organisation. Redis changed its previous license **BSD 3-Clause Model** to **Dual-License Model** (Interested Peeps can check out this news on web). What this change caused , is a born of a new project - **Valkey** (supported by Linux Foundation also)

# Redis vs Valkey ⚡
Developers who built redis under previous license came in **Valkey**. Redis under BSD , was maintained  till version 7.4x (7.4.6) which ended in October 2024. From November 2024 , Redis 8.0x series started which obeys Dual-License . On the other hand , Valkey started from v7.5x by the OG developers of redis , under BSD license.

# Features of Redis 🕶️
Have a look on the points below :
- **In-Memory**: Redis is an In-Memory product , means it stores user's data in RAM . Also we know that RAM is volatile and only necessary datas are stored inside ram which got removed when the computer shuts down. That happens with Redis also.

- **Database or not**: A contoversial point and many will consider Redis as a database also , what its documentation says **Data Structure Store - [link](https://redis.io/docs/latest/develop/get-started/data-store/)**. Although we can use redis as a document-based database but for that we need **redis-cloud** - ([link](https://redis.io/docs/latest/develop/get-started/document-database/)) . At this point you can utilize redis-cloud but remember , **redis is primarliy storing data in your device's RAM , then if you have chosen Redis-cloud , you may shift your datas to a cloud instance (sounds like mongodb-atlas but a little different)**. Else you can use **redis-om (https://redis.io/blog/introducing-redis-om-client-libraries/)** for giving a proper structure to raw datas.

- **Lua Scripting**: Lua is an lightweight language , majorly used for embedded programming. In Redis, Lua scripting enables users to write scripts that can perform complex operations directly on the server side. This means that instead of sending multiple commands from a client to the server, **users can bundle these commands into a single Lua script and execute it with one call.**

- **Data Structures and Atomicity**: Primarily redis has 9 data-structures (each will be dicussed later) where each of them has individual set of operations that used to play with datas. These sets of operations are seperate from each other which creates a layer of atomicity in redis. 

- **Pub-Sub Architechture**: Redis includes a publish/subscribe messaging paradigm, which can be used for real-time projects , offering functionality beyond simple caching.

# Installation 📋
Here is the quick installation guide :
- Install Redis based on your dependent OS from this link ➡️ [link](https://redis.io/docs/latest/operate/oss_and_stack/install/install-redis/) .
  OR
  Run the following Command (Only for Linux Users - WSL & Boot) -
  ```bash
    sudo base-pkg-manager install redis
    sudo base-pkg-manager install valkey-server #WSL
    or
    sudo base-pkg-manager install valkey #WSL
  ```

- Only for Linux (both WSL and Boot Users) run the follwing -
  ```bash
    sudo systemctl enable redis #May not work in WSL
  ```
- To start , stop and see server status for Linux users :
  
  **Boot-Linux** :
    ```bash
      sudo systemctl start <redis or valkey>
      sudo systemctl status <redis or valkey>
      sudo systemctl stop <redis or valkey>
    ```
  **WSL-Linux**:
    ```bash
      sudo service valkey-server start
      sudo service valkey-server status
      sudo service valkey-server stop
    ```
# RESP (Redis Serialization Protocol) 💻
What made redis special , is RESP . The standalone protocol , responsible for compiling commands into a format which will help the redis compiler process the user's query and create the proper output - [link](https://redis.io/docs/latest/develop/reference/protocol-spec/). What is serialize/serialization - *To tranform or hash a user-readable phrase to machine-understandable phase (not directly 0-1 but based on the rules of compilers)*. RESP is redis' own invention but developers can use it in their own projects. Prior to RESP , redis compiler breaks the whole query into chunks and maps each of chunk to a serializable format , based on the protocol and then after furthur processing the serialized output is return which got deserialized in chunks and got merged again to give the human-readable output.

# Redis Query Engine 🚒
The engine behind proper searches and queries . Redis query engine gives different excellent features consisting of vector search , full-text search , aggregation pipeline and many more. Due to RQI , redis can be used as a **vector database** , **NoSQL Document Database** and many more - [link](https://redis.io/docs/latest/develop/interact/search-and-query/)

# Data Structures ⛓️
Redis has 9 types of different data structures . Each with different taste and capabilities , given below . You can read more about them here ➡️ [link](https://redis.io/docs/latest/develop/data-types/) :

  - String
  - Hash
  - List
  - Set
  - Sorted Sets
  - Stream
  - Bitmap
  - Bitfield
  - Geospatial
    
Go to _Data Structures 📁_ to know each DS with more details

(😄 Although I suggest to visit _Storage Structure 📁_ before Data structure)
