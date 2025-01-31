# REDIS SORTED-SETS

Sorted sets are such sets where elements remain sorted . The only similarity with normal set is , elements of this set are also unique , but each of them has a score. Based on this score those values got sorted . _Sometimes if the scores match then the values got sorted based on lexicographical order (because all values are strings)_

# Commands
Every command of Sortedset has Z in the prefix . Useful commands of this data structure are :

- ## ZADD
  To add elements and their score in a sorted set , we use this command .
  
  ```bash
     127.0.0.1:6379> ZADD mysortedset 10 abc 10 abcd 9 123
     (integer) 3
  ```

- ## ZRANGE
  To get elements within a starting and Ending index of a sorted set .

  ```bash
     127.0.0.1:6379> ZRANGE mysortedset 0 -1
     1) "123"
     2) "abc"
     3) "abcd"
     127.0.0.1:6379> ZADD 10 abc
     (error) ERR wrong number of arguments for 'zadd' command
     127.0.0.1:6379> ZADD mysortedset 10 abc
     (integer) 0
     127.0.0.1:6379> ZRANGE mysortedset 0 -1 WITHSCORES      # To print Scores of the elements
     1) "123"
     2) "9"
     3) "abc"
     4) "10"
     5) "abcd"
     6) "10"
  ```

- ## ZRANGEBYSCORE
  To get elements within a range of scores of a sorted set .

  ```bash
     127.0.0.1:6379> ZRANGEBYSCORE mysortedset -inf 10
     1) "123"
     2) "abc"
     3) "abcd"
     127.0.0.1:6379> ZRANGEBYSCORE mysortedset 10 100
     1) "abc"
     2) "abcd"
  ```

- ## ZREM
  To remove element/s from a sorted set .
  
  ```bash
     127.0.0.1:6379> ZREM mysortedset abc
     (integer) 1
  ```

- ## ZREMRANGEBYSCORE
  To remove range of elements based on score .

  ```bash
     127.0.0.1:6379> ZREMRANGEBYSCORE mysortedset -inf 10
     (integer) 2
  ```
  
- ## ZRANGEBYLEX
  To get elememts within a range of lexicograhical characters .

  ```bash
     127.0.0.1:6379> ZADD mysortedset abcd 10 xyz 100 @!#$ -1
     (error) ERR value is not a valid float
     127.0.0.1:6379> ZADD mysortedset 10 abcd 100 xyz -1 @!@#$
     (integer) 3

  ```

- ## ZRANGEBYLEX
  To get elements within a range of lexicographical characters .

  ```bash
     127.0.0.1:6379> ZRANGEBYLEX mysortedset - [m
     1) "@!@#$"
     2) "abcd"
     127.0.0.1:6379> ZRANGEBYLEX mysortedset [a [m
     1) "abcd"
     127.0.0.1:6379> ZRANGEBYLEX mysortedset [a (m
     1) "abcd"
  ```

  💡For more commands , explore at here ➡️ [link](https://redis.io/docs/latest/commands/?group=sorted-set)
