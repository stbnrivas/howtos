# redis


## installation


- in fedora

```bash
sudo dnf install redis
```


- with docker without a password


```bash
docker pull redis:5.0.4
docker pull redis:alpine

docker run -it --rm -p 6379:6379 --name=redis-token-keeper redis
# or without remove automatically
docker run -it -p 6379:6379 --name=redis-token-keeper redis

docker run -it -p 6379:6379 --name sc-redis redis:5.0.5

```

- with docker _with_ a password

# TODO: it doesnt work

```bash
docker run -it --rm -p 6379:6379 --name=redis-token-keeper redis redis-server --requirepass ultrasecret

# or without remove automatically
docker run -it -p 6379:6379 --name=redis-token-keeper redis redis-server --requirepass ultrasecret
# good to know tha you can connect without password but later you need write into cli the value
AUTH ultrasecret
```

## CLI

```bash
# connect without a password
redis-cli -h $host -p $port -a $password
# default redis docker has not password ergo:
redis-cli -h localhost -p 6739
# but is very important set a password

```


## datatypes

  - Strings
    + Strings are binary safe, this means that a Redis string can contain any kind of data, for instance a JPEG image or a serialized Ruby object.
    +  String value can be at max 512 Megabytes in length.

```
SET myvalue "hello redis"
GET myvalue
```

  - Lists
    + a collection of strings sorted by insertion
    + new elements can add on the head or on the tail
```
LPUSH employee_list john
LPUSH employee_list jane
LPUSH employee_list rob
LPUSH employee_list mike

LRANGE employee_list 0 5

```
  - Hashes
    + a collections of key-values pairs, are maps between string field and string value
    + used to represents objects

```
HMSET user:1 username john password doe123 salary 20000
HGETALL user:1
```

  - Sets
    + a unordered collections of strings in redis database
    + you can test existence, add, remove elements
    + the strings has to be unique

```
SADD tasks 3456
SADD tasks 3457
SADD tasks 3458

SMEMBERS tasks
```
  - SortedSets
    + every member of a sorted set is associate wieht a score, that is used in order from the smallest to the greatest score
    + the strings are unique but the scores may be repeated

```
ZADD tutorials 1 redis-installation
ZADD tutorials 2 redis-cli
ZADD tutorials 3 troubleshooting
ZADD tutorials 4 troubleshooting-2 5 troubleshooting-3 6 troubleshooting-4

ZRANGE tutorials 0 10 WITHSCORES
```


## keys



```
DE L$keyname
EXISTS $keyname
EXPIRE $keyname $seconds
KEYS $keyname
MOVE $keyname
TTL $keyname
PERSIST $keyname
RENAME $keyname
TYPE $keyname
```

example of use key

```
SET token 'a543f234ba2e'
EXISTS token
DEL token
EXISTS token
SET token 'a543f234ba2a'
RENAME token oldtoken
KEYS *
SET token 'a543f234ba20'
MGET token oldtoken
EXPIRE token 3600
TTL token
PERSIST token
APPEND token '11111'
GET token
```


## redis string

```
SET
GET
GETRANGE $key $from $to
MGET
SETEX
SETRANGE
STRLEN
MSET
INCR
INCRBY
DECR
DECRBY
APPEND
```

# redis hashes

```
HDEL
HEXIST
HGET
HGETALL
HINCRBY
HKEYS
HLEN
HMGET
HVALS
```
