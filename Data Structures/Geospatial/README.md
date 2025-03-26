# Redis Geospatial
Redis provides built-in support for geospatial data, allowing you to store, retrieve, and query locations efficiently.

## Properties
- Redis uses the **Geohash** technique to store location data.
- Uses a single key to store multiple location coordinates.
- Supports radius-based queries and distance calculations.

## Commands

### **GEOADD**
Adds geospatial data (longitude, latitude, and member name) to a key.

```sh
127.0.0.1:6379> GEOADD locations 13.361389 38.115556 "Palermo"
OK
127.0.0.1:6379> GEOADD locations 15.087269 37.502669 "Catania"
OK
```

### **GEOPOS**
Fetches the coordinates of a given location.

```sh
127.0.0.1:6379> GEOPOS locations "Palermo"
1) ("13.361389", "38.115556")
```

### **GEODIST**
Calculates the distance between two locations.

```sh
127.0.0.1:6379> GEODIST locations "Palermo" "Catania" km
"166.2747"
```

### **GEORADIUS** (Deprecated, use `GEOSEARCH`)
Finds locations within a given radius from a point.

```sh
127.0.0.1:6379> GEORADIUS locations 15 37 200 km
1) "Catania"
2) "Palermo"
```

### **GEOSEARCH**
Finds locations by radius or bounding box.

```sh
127.0.0.1:6379> GEOSEARCH locations FROMLONLAT 15 37 BYRADIUS 200 km
1) "Catania"
2) "Palermo"
```

### **GEOHASH**
Retrieves the geohash string for a location.

```sh
127.0.0.1:6379> GEOHASH locations "Palermo"
1) "sqc8b49rny0"
```

### **GEODEL**
To remove a specific location from a geospatial set, use `DEL`.

```sh
127.0.0.1:6379> DEL locations
(integer) 1
```

## Additional Information
For more details on Redis geospatial commands, visit the [official Redis documentation](https://redis.io/commands#geo).


