# REDIS LISTS

To implement **stack** and **queue** in redis , we use **list** data structure . Redis lists can be used as **backgound workers**
for an app .

# Commands
Notable Lists commands are used in the snippets below :

- ## LPUSH & LRANGE

  ```bash
     127.0.0.1:6379> LPUSH mystack house
     (integer) 1
     127.0.0.1:6379> LPUSH mystack car
     (integer) 2
     127.0.0.1:6379> LLEN mystack
     (integer) 2
     127.0.0.1:6379> LRANGE mystack 0 2
     1) "car"
     2) "house"
     127.0.0.1:6379> LPUSH mystack 10
     (integer) 3
     127.0.0.1:6379> LPUSH mystack True
     (integer) 4
  ```
  
- ## RPUSH

  ```bash
     127.0.0.1:6379> RPUSH myqueue car house
     (integer) 2
     127.0.0.1:6379> LRANGE myqueue 0 2
     1) "car"
     2) "house"
  ```
- ## LPOP

  ```bash
     127.0.0.1:6379> LPOP myqueue
     "car"
     127.0.0.1:6379> LPOP myqueue
     "house"
  ```
- ## RPOP

  ```bash
     127.0.0.1:6379> RPOP mystack
     "house"
     127.0.0.1:6379> RPOP mystack
     "car"
     127.0.0.1:6379> RPOP mystack  2
     1) "10"
     2) "True"
  ```
- ## LLEN
  
  ```bash
     127.0.0.1:6379> LLEN mystack
     (integer) 3
  ```
- ## LMOVE

  ```bash
     127.0.0.1:6379> LPUSH mystack places
     (integer) 1
     127.0.0.1:6379> LMOVE myqueue mystack RIGHT LEFT
     "car"
     127.0.0.1:6379> LRANGE mystack 0 2
     1) "car"
     2) "places"
     127.0.0.1:6379> LMOVE myqueue mystack RIGHT LEFT
     "house"
     127.0.0.1:6379> LRANGE mystack 0 2
     1) "house"
     2) "car"
     3) "places"
  ```
- ## LTRIM
- ## BLPOP
- ## BLMOVE

To know more about _list commands_ , explore here ➡️ [link](https://redis.io/docs/latest/commands/?group=list)
