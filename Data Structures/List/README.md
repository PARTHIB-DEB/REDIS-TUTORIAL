# REDIS LISTS

To implement **stack** and **queue** in redis , we use **list** data structure . Redis lists can be used as **backgound workers**
for an app .

# Commands
Notable Lists commands are used in the snippets below :

- ## LPUSH & LRANGE
  
  To Add elements in a LIST from LEFT , we use LPUSH
  
  To GET elements of a LIST in a certain RANGE OF INDICES , we use LRANGE

  ```bash
     127.0.0.1:6379> LPUSH mystack house
     (integer) 1
     127.0.0.1:6379> LPUSH mystack car
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

  To Add elements in a LIST from RIGHT , we use RPUSH

  ```bash
     127.0.0.1:6379> RPUSH myqueue car house
     (integer) 2
     127.0.0.1:6379> LRANGE myqueue 0 2
     1) "car"
     2) "house"
  ```
  
- ## LPOP

  To Remove elements in a LIST from LEFT , we use LPOP

  ```bash
     127.0.0.1:6379> LPOP myqueue
     "car"
     127.0.0.1:6379> LPOP myqueue
     "house"
  ```
  
- ## RPOP

  To Remove elements in a LIST from RIGHT , we use RPOP

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

  To measure LENGTH of a LIST , we use LLEN
  
  ```bash
     127.0.0.1:6379> LLEN mystack
     (integer) 3
  ```
  
- ## LMOVE

  To shift elements from LIST TO LIST , we use LMOVE .
  Arguments in LMOVE - 2 list names , Side of removal from prior and side of append in later list

  ```bash
     127.0.0.1:6379> LPUSH mystack places
     (integer) 1
     127.0.0.1:6379> LMOVE myqueue mystack RIGHT LEFT    # myqueue(RIGHT) --> mystack(LEFT)
     "car"
     127.0.0.1:6379> LRANGE mystack 0 2
     1) "car"
     2) "places"
     127.0.0.1:6379> LMOVE myqueue mystack RIGHT LEFT    # myqueue(RIGHT) --> mystack(LEFT)
     "house"
     127.0.0.1:6379> LRANGE mystack 0 2
     1) "house"
     2) "car"
     3) "places"
  ```
- ## LTRIM

  To trim the LIST , we use LTRIM .

  It takes range of indices - the remaining part will be trimmed.

  ```bash
     127.0.0.1:6379> LRANGE mystack 0 2
     1) "house"
     2) "car"
     3) "places"
     127.0.0.1:6379> LTRIM mystack 0 1        # Oth and 1th elements will be there only
     OK
     127.0.0.1:6379> LRANGE mystack 0 2
     1) "house"
     2) "car"
     127.0.0.1:6379> LTRIM mystack 1 2        # 1th and 2nd(empty) elements will be there only
     OK
     127.0.0.1:6379> LRANGE mystack 0 1
     1) "car"
     127.0.0.1:6379> LRANGE mystack 0 2
     1) "car"
  ```
- ## BLPOP

  Blocks LPOP operation upto certain timelimits and then LPOP happens .
  It just takes the time-limits as arguments and POPS from Leftside after that time-limits expire

  ```bash
     127.0.0.1:6379> BLPOP mystack 1
     (nil)
     (1.04s)
     127.0.0.1:6379> BLPOP myqueue 1
     1) "myqueue"
     2) "car"
     127.0.0.1:6379> BLPOP myqueue 4
     1) "myqueue"
     2) "car"
     127.0.0.1:6379> BLPOP myqueue 90
     1) "myqueue"
     2) "torch"
     127.0.0.1:6379> BLPOP myqueue 1
     1) "myqueue"
     2) "bus"
     127.0.0.1:6379> BLPOP myqueue 10
     1) "myqueue"
     2) "1"
     127.0.0.1:6379> LRANGE myqueue 0 5
     1) "2"
  ```
  
- ## BLMOVE

  Blocks LMOVE operation upto certain timelimits and then LMOVE happens

  ```bash
     127.0.0.1:6379> RPUSH mystack car torch bus 1 2        # Create the list again
     (integer) 6
     127.0.0.1:6379> LRANGE mystack 0 6
     1) "car"
     2) "car"
     3) "torch"
     4) "bus"
     5) "1"
     6) "2"
     127.0.0.1:6379> LRANGE mystack 0 5
     1) "car"
     2) "car"
     3) "torch"
     4) "bus"
     5) "1"
     127.0.0.1:6379> BLMOVE mystack myqueue LEFT RIGHT 2          # Block LMOVE untill 2 seconds gone 
     "car"
     127.0.0.1:6379> LRANGE myqueue 0 2
     1) "car"
     127.0.0.1:6379> BLMOVE mystack myqueue LEFT RIGHT 6          # Block LMOVE untill 6 seconds gone
     "car"
     127.0.0.1:6379> LRANGE myqueue 0 2
     1) "car"
     2) "car"
     127.0.0.1:6379> LRANGE myqueue 0 6
     1) "car"
     2) "car"
     127.0.0.1:6379> BLMOVE mystack myqueue LEFT RIGHT 100
     "torch"
     127.0.0.1:6379> LRANGE myqueue 0 6
     1) "car"
     2) "car"
     3) "torch"
     127.0.0.1:6379> BLMOVE mystack myqueue LEFT RIGHT 1000
     "bus"
     127.0.0.1:6379> LRANGE myqueue 0 6
     1) "car"
     2) "car"
     3) "torch"
     4) "bus"
     127.0.0.1:6379> BLMOVE mystack myqueue LEFT RIGHT 1000
     "1"
     127.0.0.1:6379> LRANGE myqueue 0 6
     1) "car"
     2) "car"
     3) "torch"
     4) "bus"
     5) "1"
     127.0.0.1:6379> BLMOVE mystack myqueue LEFT RIGHT 10000         # will happen in blink of an eye , dear :) !!
     "2"
     127.0.0.1:6379> LRANGE myqueue 0 6
     1) "car"
     2) "car"
     3) "torch"
     4) "bus"
     5) "1"
     6) "2"
     127.0.0.1:6379> BLMOVE mystack myqueue LEFT RIGHT 10              # Block LMOVE untill 10 seconds gone
     (nil)
     (10.03s)
  ```

To know more about _list commands_ , explore here ➡️ [link](https://redis.io/docs/latest/commands/?group=list)
