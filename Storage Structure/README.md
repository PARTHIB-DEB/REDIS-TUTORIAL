# REDIS STORAGE STRUCTURE

- We already know , redis can be treated as a *Document based NoSQL Database* . Yet , the difference is , it has no specific query sentence. Instead of that , redis uses **keywords**.

- Redis stores data as _Key-Value Pairs_ . Now , it can be individual pair or a nested chain of pairs. Redis keys are always of datatype **String** . What changes , is the datatype of values.

- By default , redis stores the data in server running at port **6379**

# Basic Redis Commands

The snippet explains a general way to create , save and update user's data.

```bash
  127.0.0.1:6379> SET 1 "100"   # SET the value of key "1"
  OK
  127.0.0.1:6379> GET 1     # GET the value of key "1"
  "100"
  127.0.0.1:6379> TYPE 1     # Type of KEY - 1 (always string)
  string
  127.0.0.1:6379> TYPE 100    # Can't use TYPE for values , there is no key "100"
  none
  127.0.0.1:6379> SET 1 10000    # Updating the value of key "1" using SET
  OK
  127.0.0.1:6379> GET 1          # Again Fetching Value of Key 1
  "10000"
  127.0.0.1:6379> INCRBY 1 5      # INCRBY - a keyword , works on INTEGER values . Hence works on key "1"
  (integer) 10005
  127.0.0.1:6379> GET 1          # Again Fetching Value of Key 1
  "10005"
```
Many of you will question , why value of 1 is showing in "" 🤔 - Good Question. Remember , RESP is constantly working behind. So , indeed the value of key 1 is INTEGER , but when its being displayed in the screen by GET - Its typecasting to string is happening temporarily.
