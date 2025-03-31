# REDIS STREAMS

A Redis stream is a data structure that acts like an append-only log but also implements several operations to overcome some of the limits of a typical append-only log. It stores different blocks, which are just key-value pairs, linked to a stream key. Redis generates a unique ID for each stream entry, allowing you to retrieve associated entries later or read and process all subsequent entries in the stream.

❗ Note that because these IDs are related to time, the ones shown here may vary and will be different from the IDs you see in your own Redis instance.

To understand **Streams**, read the content here ➡️ [link](https://medium.com/redis-with-raphael-de-lio/understanding-redis-streams-33aa96ca7206)

## Use Cases

You can use streams to record and simultaneously syndicate events in real time. Examples of Redis stream use cases include:

- **Event Sourcing**: Tracking user actions, clicks, and other events.
- **Sensor Monitoring**: Collecting readings from devices in the field.
- **Notifications**: Storing a record of each user's notifications in a separate stream.
- **Data Pipelines**: Streaming data from one service to another in real-time.
- **Chat Applications**: Storing messages in a chat application for real-time access.

## Important Commands

### XADD
To add different blocks in a stream.

```bash
127.0.0.1:6379> XADD mystreamkey * temp 45 city "kolkata"
"1739981330599-0"
```

### XRANGE
To get a range of blocks of a stream.

```bash
127.0.0.1:6379> XRANGE mystreamkey 1739981330599-0 + COUNT 2
1) 1) "1739981330599-0"
   2) 1) "temp"
      2) "45"
      3) "city"
      4) "kolkata"
```

### XLEN
To get the length of a stream key (number of blocks in a stream).

```bash
127.0.0.1:6379> XLEN mystreamkey
(integer) 1
```

### XREAD
To read data from one or more streams.

```bash
127.0.0.1:6379> XREAD COUNT 2 STREAMS mystreamkey 0
```

### XREVRANGE
To get a range of blocks in reverse order.

```bash
127.0.0.1:6379> XREVRANGE mystreamkey + - COUNT 2
1) 1) "1739981330599-0"
   2) 1) "temp"
      2) "45"
      3) "city"
      4) "kolkata"
```

### XGROUP
To create a consumer group for the stream.

```bash
127.0.0.1:6379> XGROUP CREATE mystreamkey mygroup 0
```

### XACK
To acknowledge messages in a consumer group.

```bash
127.0.0.1:6379> XACK mystreamkey mygroup 1739981330599-0
```

### XREADGROUP
To read data from a stream as part of a consumer group.

```bash
127.0.0.1:6379> XREADGROUP GROUP mygroup Alice STREAMS mystreamkey >
```

## Explore More Commands
For a comprehensive list of Redis Stream commands, visit [Redis Commands Documentation](https://redis.io/docs/latest/commands/?group=stream).
