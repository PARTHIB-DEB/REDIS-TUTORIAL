# REDIS STREAMS

An append-only log is a data structure where new data is added to the end (appended) but existing data cannot be modified or deleted

A Redis stream is a data structure that acts like an append-only log but also implements several operations to overcome some of the limits of a typical append-only log. 

Redis generates a unique ID for each stream entry. You can use these IDs to retrieve their associated entries later or to read and process all subsequent entries in the stream. 

❗ Note that because these IDs are related to time, the ones shown here may vary and will be different from the IDs you see in your own Redis instance.

# Usecases

You can use streams to record and simultaneously syndicate events in real time. Examples of Redis stream use cases include:

- Event sourcing (e.g., tracking user actions, clicks, etc.)
- Sensor monitoring (e.g., readings from devices in the field)
- Notifications (e.g., storing a record of each user's notifications in a separate stream)

# Commands

Important STREAMS commands are - 

