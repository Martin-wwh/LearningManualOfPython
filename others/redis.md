## 简介
redis与其他key-value缓存产品相比较的特点:
- Redis支持数据持久化，可以将内存中的数据存在磁盘中，重启时可以再次加载使用
- Redis不仅支持简单的key-value类型的数据，同时还提供list,set,zset,hash等数据结构的存储
- Redis支持数据备份，即master-slave模式的数据备份

## Redis优势
- 性能极高-Redis能读的速度1100000次/s，写是81000次/s
- 丰富的数据类型
- 原子-Redis的所有操作都是原子性的。单个操作是原子性的。多个操作也支持事务
- 丰富的特性-Redis还支持publish/subscribe，通知，key过期等特性。

## Redis配置
通过config命令查看或设置配置项

redis.conf的配置项说明:

|序号|配置项|说明|
|---|----|----|
|1|daemonize no|redis默认不是以守护进程运行，可以通过修改该配置项为yes启动守护进程(windows不支持)|
|2|pidfile /var/run/pidfile|redis以守护进程运行时，默认会将pid写入pidfile|
|3|port 6379|指定redis监听端口,6379是默认端口号|
|4|bind 127.0.0.1|绑定主机地址|
|5|timeout 300|指定客户端闲置多少秒后关闭连接，如果指定为0，表示关闭该功能|
|6|loglevel notice|指定日志记录级别，总共四个级别:debug、verbose、notice、warning,默认notice|
|7|logfile stdout|日志记录方式,默认为标准输出|
|8|databases 16|设置数据库的数量,默认数据库为0，可以用select命令在连接上指定数据库id|
|9|save <seconds> <changes>|指定多长时间有多少次更新操作就把数据同步到数据文件，可以多个条件配合|
|10|rdbcompression yes|指定存储到本地数据库时是否压缩数据，redis采用LZF压缩|
|11|dbfilename dump.rdb|指定本地数据库文件名，默认值为dump.rdb|
|12|dir .|指定本地数据库存放目录|

#### Redis数据类型
五种数据类型：string,hash,list,set,zset

string是二进制安全的。即redis的string可以包含任何数据。如jpg图片或序列化的对象。最大可以存储512M。

hash是一个键值对集合，是一个string类型的field和value的映射表，hash特别适合存储对象。

HMSET设置field=>value对, HGET获取对应field对应的value。

每个hash可以存储232 -1键值对(40多亿)。

Redis的set是string类型的无序集合。集合是通过哈希表实现的，所以添加、删除、查找的复杂度都是O(1)

zset是有序集合。zset每个元素都会关联一个double类型的分数。redis是通过分数来给集合中的成员排序，zset的成员是唯一的，但是用于排序的分数可以重复。


#### Redis命令
客户端基本语法：

redis-cli -h host -p port -a passwd

#### Redis键(Key)
redis键命令的基本语法：

COMMAND KEY_NAME
 
#### Redis字符串的命令

|命令|描述|
|---|---|
|set key value|设置指定key的值|
|get key| |
|getrange key start end|获取key从start到end的子串，包含头尾|
|getset key value|将给定key置为value，并将旧值返回|
|mget key1 [key2..]|返回所有给定的key值|
|setex key