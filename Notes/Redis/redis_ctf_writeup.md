# Redis In-Memory Database - CTF Walkthrough

## What is Redis?

Redis is an in-memory data structure store commonly used as a cache, session store, or message broker. It stores data in RAM for extremely fast access, making it popular for performance-critical applications.

## Key Concepts for CTF Challenges

### Data Structure Types

Redis supports multiple data types that challenges often exploit:
- **Strings**: Simple key-value pairs
- **Lists**: Ordered collections of strings
- **Sets**: Unordered unique collections
- **Hashes**: Maps of field-value pairs
- **Sorted Sets**: Sets with associated scores

### Common Vulnerabilities

**Unauthenticated Access**: Redis often runs with default settings that allow anyone to connect without authentication, leading to data exposure or manipulation.

**No Encryption**: Data in transit and at rest is typically unencrypted, making it vulnerable to eavesdropping.

**Direct Data Access**: If you can connect to Redis, you can directly read all stored data—no SQL injection or complex queries needed.

## Connecting to Redis

Redis typically runs on port 6379. You can interact with it using:

```bash
redis-cli -h <host> -p <port>
```

## Common Redis Commands for CTF

```bash
PING                           # Test connection
INFO                           # Server information
DBSIZE                         # Number of keys
KEYS *                         # List all keys
GET <key>                      # Retrieve string value
HGETALL <key>                  # Get all fields in a hash
LRANGE <key> 0 -1             # Get all items in a list
SMEMBERS <key>                # Get all members in a set
ZRANGE <key> 0 -1             # Get all members in sorted set
FLUSHDB                        # Clear current database
SELECT <db>                    # Switch to different database
```

## CTF Challenge Patterns

**Exposed Credentials**: Flags or credentials stored as Redis keys.

**Multiple Databases**: Redis supports 16 databases by default (0-15). Challenge data might be in a non-default database.

**Data Enumeration**: Use `KEYS *` to discover what data is stored, then retrieve it with appropriate commands.

**Session Data**: Look for serialized session objects that might contain sensitive information.

## Security Considerations

- Redis should never be exposed to untrusted networks without authentication
- Enable `requirepass` to require a password for connections
- Use firewalls to restrict access to the Redis port
- Implement encryption for sensitive data at the application level