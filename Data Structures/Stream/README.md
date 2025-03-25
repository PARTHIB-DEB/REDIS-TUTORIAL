# REDIS STREAMS

An append-only log is a data structure where new data is added to the end (appended) but existing data cannot be modified or deleted

A Redis stream is a data structure that acts like an append-only log but also implements several operations to overcome some of the limits of a typical append-only log. Means It stores diffent blocks , which are just key-value pairs . Thus, many blocks got linked to a stream key

Redis generates a unique ID for each stream entry. You can use these IDs to retrieve their associated entries later or to read and process all subsequent entries in the stream. 

❗ Note that because these IDs are related to time, the ones shown here may vary and will be different from the IDs you see in your own Redis instance.

To Understand **Streams** , read the content here ➡️ [link](https://medium.com/redis-with-raphael-de-lio/understanding-redis-streams-33aa96ca7206)

# Usecases

You can use streams to record and simultaneously syndicate events in real time. Examples of Redis stream use cases include:

- Event sourcing (e.g., tracking user actions, clicks, etc.)
- Sensor monitoring (e.g., readings from devices in the field)
- Notifications (e.g., storing a record of each user's notifications in a separate stream)

# Commands

Important STREAMS commands are - 

## XADD
To add different blocks in a stream

```bash
  127.0.0.1:6379> XADD mystreamkey * temp 45 city "kolkata"
  "1739981330599-0"
```

## XRANGE
To get a range of blocks of a stream

```bash
    127.0.0.1:6379> XRANGE mystreamkey 1739981330599-0 + COUNT 2
    1) 1) "1739981330599-0"
       2) 1) "temp"
          2) "45"
          3) "city"
          4) "kolkata"
    127.0.0.1:6379> XRANGE mystreamkey 1739981330600-0 + COUNT 2
    (empty array)
    127.0.0.1:6379> XRANGE mystreamkey 1739981330500-0 + COUNT 2
    1) 1) "1739981330599-0"
       2) 1) "temp"
          2) "45"
          3) "city"
          4) "kolkata"
```

## XLEN
To get the length of a stream key (no of blocks in a stream)

```bash
    127.0.0.1:6379> XLEN mystreamkey
    (integer) 1
```
