Redis Data Structures: In-Depth Guide with Use Cases & Code Example
## 1. Strings

**Description**: Basic key-value storage for text, numbers, or binary data (up to 512MB)

**Use Cases**:

- Caching HTML fragments or API responses
    
- Counter implementations (views, likes)
    
- Session storage
    
- Simple flags or feature toggles
    

**Key Commands**:

```
bash

SET key value [EX seconds] [NX|XX]  # Store value with optional TTL and conditions
GET key                            # Retrieve value
INCR key                           # Atomic increment
DECR key                           # Atomic decrement
MSET key1 value1 key2 value2       # Set multiple keys
MGET key1 key2                     # Get multiple values
```

**Python Example**:

```
python

import redis

r = redis.Redis(host='localhost', port=6379, db=0)
```

# Basic string operations
```
r.set('user:1000:name', 'John Doe', ex=3600)  # Set with 1-hour expiration
name = r.get('user:1000:name')                # Retrieve value
```

# Counters
```
r.set('page:home:views', 0)
r.incr('page:home:views')                     # Atomic increment
views = r.get('page:home:views')
```
## 2. Hashes

**Description**: Field-value maps perfect for storing objects

**Use Cases**:

- User profiles with multiple attributes
    
- Product catalogs
    
- Configuration objects
    
- Storing related properties together
    

**Key Commands**:

```
bash

HSET key field value [field value ...]  # Set one or multiple fields
HGET key field                         # Get specific field
HGETALL key                            # Get all fields and values
HINCRBY key field increment           # Increment field by integer
HDEL key field [field ...]            # Delete one or more fields
```

**Python Example**:

```
python

# Store user object
r.hset('user:1000', mapping={
    'name': 'Alice',
    'email': 'alice@example.com',
    'age': '28'
})

# Get all user data
user_data = r.hgetall('user:1000')
# Returns: {b'name': b'Alice', b'email': b'alice@example.com', b'age': b'28'}

# Increment age
r.hincrby('user:1000', 'age', 1)
```

## 3. Lists

**Description**: Ordered collection of strings (insertion order)

**Use Cases**:

- Message queues (FIFO)
    
- Activity feeds
    
- Recent items history
    
- Task queues for workers
    

**Key Commands**:

```
bash

LPUSH key value [value ...]   # Add to beginning of list
RPUSH key value [value ...]   # Add to end of list
LPOP key                     # Remove and get first element
RPOP key                     # Remove and get last element
LRANGE key start stop        # Get range of elements
LTRIM key start stop         # Trim list to specified range
```
**Python Example**:

```
python

# Implement a message queue
r.lpush('message:queue', 'task1')
r.lpush('message:queue', 'task2')

# Process messages (FIFO)
while True:
    task = r.rpop('message:queue')
    if not task:
        break
    process_task(task)

# Recent activity feed
r.lpush('user:1000:activity', 'Logged in')
r.lpush('user:1000:activity', 'Viewed profile')
r.ltrim('user:1000:activity', 0, 49)  # Keep only 50 most recent activities
```

## 4. Sets

**Description**: Unordered collection of unique strings

**Use Cases**:

- Tagging systems
    
- Unique user tracking
    
- Voting systems (prevent duplicate votes)
    
- Friend relationships in social networks
    

**Key Commands**:

```
bash

SADD key member [member ...]   # Add one or more members
SREM key member [member ...]   # Remove one or more members
SISMEMBER key member           # Check if member exists
SMEMBERS key                   # Get all members
SINTER key1 key2               # Intersection of multiple sets
SUNION key1 key2               # Union of multiple sets
```

**Python Example**:

```
python

# Tagging system
r.sadd('article:1000:tags', 'technology', 'programming', 'redis')
r.sadd('article:1001:tags', 'programming', 'python')

# Find common tags between articles
common_tags = r.sinter('article:1000:tags', 'article:1001:tags')
# Returns: {b'programming'}

# Check if user has voted
if not r.sismember('poll:1000:voters', 'user:1000'):
    r.sadd('poll:1000:voters', 'user:1000')
    r.incr('poll:1000:votes')
```

## 5. Sorted Sets

**Description**: Sets with each member having a score for ordering

**Use Cases**:

- Leaderboards and rankings
    
- Priority queues
    
- Time-series data
    
- Rate limiting with sliding windows
    

**Key Commands**:

```
bash

ZADD key score member [score member ...]  # Add members with scores
ZRANGE key start stop [WITHSCORES]       # Get range by index (ascending)
ZREVRANGE key start stop [WITHSCORES]    # Get range by index (descending)
ZRANGEBYSCORE key min max [WITHSCORES]   # Get range by score
ZRANK key member                         # Get member's rank (ascending)
ZREVRANK key member                      # Get member's rank (descending)
```
**Python Example**:

```
python

# Leaderboard implementation
r.zadd('game:leaderboard', {
    'player1': 1000,
    'player2': 1500,
    'player3': 750
})

# Update score
r.zincrby('game:leaderboard', 100, 'player1')

# Get top 3 players
top_players = r.zrevrange('game:leaderboard', 0, 2, withscores=True)
# Returns: [(b'player2', 1500.0), (b'player1', 1100.0), (b'player3', 750.0)]

# Get player rank
rank = r.zrevrank('game:leaderboard', 'player1')  # Returns 1 (0-indexed)
```
## 6. HyperLogLog

**Description**: Probabilistic data structure for cardinality estimation

**Use Cases**:

- Unique visitor counting
    
- Distinct element counting in large datasets
    
- Analytics where approximate counts are acceptable
    

**Key Commands**:

```
bash

PFADD key element [element ...]   # Add elements to HyperLogLog
PFCOUNT key [key ...]            # Get approximate count of elements
PFMERGE destkey sourcekey [sourcekey ...]  # Merge multiple HyperLogLogs
```
**Python Example**:
```
python

# Track unique daily visitors
r.pfadd('visitors:2023-10-01', '192.168.1.1', '192.168.1.2', '192.168.1.1')

# Get approximate count
count = r.pfcount('visitors:2023-10-01')
# Returns: 2 (unique IPs, ignoring duplicates)

# Merge daily counts to get weekly count
r.pfmerge('visitors:2023-10-01-07', 'visitors:2023-10-01', 'visitors:2023-10-02')
weekly_count = r.pfcount('visitors:2023-10-01-07')
```

## 7. Geospatial Indexes

**Description**: Sorted sets with geospatial data

**Use Cases**:

- Location-based services
    
- Find nearby points of interest
    
- Delivery radius calculations
    
- Ride-sharing applications

**Key Commands**:

```
bash

GEOADD key longitude latitude member [longitude latitude member ...]  # Add locations
GEOSEARCH key FROMMEMBER member [FROMLONLAT longitude latitude] [BYRADIUS radius unit] [ASC|DESC] [COUNT count]  # Search locations
GEODIST key member1 member2 [unit]  # Distance between two members
GEOHASH key member [member ...]     # Get Geohash string for members
```

**Python Example**:

```
python

# Add locations
r.geoadd('restaurants:locations', 
    -73.935242, 40.730610, 'Restaurant A',
    -73.989998, 40.733998, 'Restaurant B'
)

# Find restaurants within 5km of a point
nearby = r.geosearch('restaurants:locations', 
    longitude=-73.9667, latitude=40.78, 
    radius=5, unit='km', withdist=True
)

# Returns: [(b'Restaurant A', 3.2145), (b'Restaurant B', 4.8762)]
```

## 8. Bitmaps

**Description**: String type that lets you work with individual bits

**Use Cases**:

- Feature flags for users
    
- Daily activity tracking
    
- Real-time analytics
    
- Efficient boolean arrays
    

**Key Commands**:

bash

SETBIT key offset value     # Set or clear bit at offset
GETBIT key offset          # Get bit value at offset
BITCOUNT key [start end]   # Count set bits
BITOP operation destkey key [key ...]  # Bitwise operations between keys

**Python Example**:

```
python

# User feature flags (each bit represents a feature)
USER_FEATURES = {
    'PREMIUM': 0,
    'EMAIL_VERIFIED': 1,
    'SMS_VERIFIED': 2
}

# Set premium feature for user 1000
r.setbit('user:1000:features', USER_FEATURES['PREMIUM'], 1)

# Check if user has premium
is_premium = r.getbit('user:1000:features', USER_FEATURES['PREMIUM'])

# Daily active users tracking
import datetime
today = datetime.date.today().isoformat()
r.setbit(f"active:users:{today}", user_id, 1)

# Count active users today
active_count = r.bitcount(f"active:users:{today}")
```

## 9. Streams

**Description**: Append-only log data structure for event sourcing

**Use Cases**:

- Message brokering
    
- Event sourcing
    
- Audit logs
    
- Real-time data processing
    

**Key Commands**:

```
bash

XADD key [NOMKSTREAM] [MAXLEN|MINID [=|~] threshold [LIMIT count]] *|ID field value [field value ...]  # Add entry to stream
XREAD [COUNT count] [BLOCK milliseconds] STREAMS key [key ...] ID [ID ...]  # Read entries from streams
XGROUP CREATE key groupname ID|$ [MKSTREAM]  # Create consumer group
XREADGROUP GROUP group consumer [COUNT count] [BLOCK milliseconds] [NOACK] STREAMS key [key ...] ID [ID ...]  # Read as consumer group
```
**Python Example**:

```
python

# Add event to stream
r.xadd('user:events', {
    'type': 'login',
    'user_id': '1000',
    'timestamp': '2023-10-01T10:00:00Z'
})

# Create consumer group
try:
    r.xgroup_create('user:events', 'logging_group', '$', mkstream=True)
except redis.ResponseError:
    # Group might already exist
    pass

# Read events as consumer
events = r.xreadgroup('logging_group', 'consumer1', {'user:events': '>'}, count=1, block=5000)

# Process events
for stream, messages in events:
    for message_id, message in messages:
        process_event(message)
        r.xack('user:events', 'logging_group', message_id)  # Acknowledge processing
```

## Choosing the Right Data Structure

|Data Structure|Best For|Performance|Memory Efficiency|
|---|---|---|---|
|Strings|Simple values, counters|O(1) for access|Moderate|
|Hashes|Objects, multiple fields|O(1) per field|High for many small fields|
|Lists|Queues, timelines|O(1) for push/pop|High|
|Sets|Unique items, relationships|O(1) for adds/checks|Moderate|
|Sorted Sets|Rankings, ranges|O(log N) for operations|Low|
|HyperLogLog|Cardinality estimation|O(1)|Very High|
|Bitmaps|Boolean arrays, flags|O(1)|Extremely High|
|Streams|Event logging, messaging|O(1) for appends|Moderate|
