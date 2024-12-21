# REDIS-TUTORIAL [![My Skills](https://simpleskill.icons.workers.dev/svg?i=redis)](https://redis.io/) [![My Skills](https://skillicons.dev/icons?i=redis)](https://redis.io/)
Redis - Remote Dictionary Server . Built by Salvatore Sanfilippo (known as antirez) in 2009. **Redis Labs** (Previously knew as **Garantia Data**) , is the organisation which maintains redis.

# Major changes in 2024 💡
Maybe some of us has got a recent spiced up news of redis's sudden license change which created an internal conflict within the organisation. Redis changed its previous license **BSD 3-Clause Model** to **Dual-License Model** (Interested Peeps can check out this news on web). What this change caused , is a born of a new project - **Valkey** (supported by Linux Foundation also)

# Redis vs Valkey ⚡
Developers who built redis under previous license came in **Valkey**. Redis under BSD , was maintained  till version 7.4x (7.4.6) which ended in October 2024. From November 2024 , Redis 8.0x series started which obeys Dual-License . On the other hand , Valkey started from v7.5x by the OG developers of redis , under BSD license.

# Features of Redis 🕶️
Have a look on the points below :
- **In-Memory**: Redis is an In-Memory product , means it stores user's data in RAM . Also we know that RAM is volatile and only necessary datas are stored inside ram which got removed when the computer shuts down. That happens with Redis also.

- **Database or not**: A contoversial point and many will consider Redis as a database also , but what its documentation says **Data Structure Store - [link](https://redis.io/docs/latest/develop/get-started/data-store/)**. That simply means Redis uses its own data structres to store data - It doesn't tell any thing about schema or document or storing in SSD/HDDs like normal DBs. Even though you can use libraries like **Redis-Om - [link](https://redis.io/blog/introducing-redis-om-client-libraries/)** which helps to decorate raw data in a format , yet that doesn't define anything on behalf of Redis , but if you are using redis' 8.0x versions then you may get some features where redis will take snapshots of user's data and will put them in SSD/HDDs. 

- **Lua Scripting**:

- **Data Structures and Atomicity**

# Installation 📋

# RESP (Redis Serialization Protocol) 💻

# Data Structures ⛓️
