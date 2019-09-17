<!-- GFM-TOC -->
* ### [一、简介](#一简介-1)
* ### [二、数据类型](#二数据类型)
    * ### [String](#string-1)
    * ### [List](#list-1)
    * ### [Set](#set-1)
    * ### [Hash](#hash-1)
    * ### [Sorted Set](#sorted-set-1)
* ### [三、发布订阅](#三发布订阅-1)
* ### [四、键的过期时间](#四键的过期时间-1)
* ### [五、数据淘汰策略](#五数据淘汰策略-1)
* ### [六、持久化](#六持久化-1)
* ### [七、事物](#七事物-1)
* ### [八、事件](#八事件-1)
* ### [九、集群](#九集群-1)
* ### [十、应用场景](#十应用场景-1)
<!-- GFM-TOC -->

# 一、简介
Redis:速度快、非关系型(NOSQL)、内存键值型数据库，单线程。

键的类型只能为字符串,值支持五种数据类型：字符串、列表、集合、散列表、有序集合。

Redis支持内存数据持久化到硬盘、使用复制来扩展读性能、使用分片来扩展写性能等特性。

# 二、数据类型
- ### String
    * 可存储的值：字符串、整数、浮点数
    
    * 操作：对字符串或其一部分进行操作、对整数和浮点数进行自增或自减操作
    
    * 命令：
        - **set key value** 设置指定key的值 
           
        - **get key** 获取key的值
        
        - **getrange key start end** 返回key中字符串的子字符串
        
        - **getset key value** 将给定的key的值设为value，并返回key的旧值
        
        - **getbit key offset** 对key所存储的字符串值，获取指定偏移量上的位 
        
        - **mget key...** 获取一个或多个key的值
        
        - **setex key seconds value** 设置key的值为value，并且设置key的过期时间位senconds(秒)
        
        - **setnx key value** 只有在key不存在时设置key的值
        
        - **strlen key** 返回key所存储字符串的长度
        
        - **mset key value [key value ...]** 同时设置一个或多个key-value
        
        - **msetnx key value [key value ...]** 同时设置一个或多个key-value,当且仅当所有给定的key都不存时
        
        - **psetex key millseconds value** 设置key的值为value，并且设置key的过期时间位millseconds(毫秒)
        
        - **incr key** 将key所存储的数字值增加1
        
        - **incrby key increment** 将key所存储的值加上给定的增量值(increment)
        
        - **incrbyfloat key increment** 将key所存储的值加上给定的浮点增量值(increment)
        
        - **decr key** 将key中存储的数字减一
        
        - **decrby key decrement** key中所存储的值减去给定的减量值(decrement)
        
        - **append key value** 如果key已经存在并且是一个字符串,将指定的value追加到原来值的末尾。
    - 使用场景：


    
- ### List
    * 可存储的值：列表
    
    * 操作：从两端压入或弹出元素、 对单个元素或这多个元素进行修剪，只保留一个范围内的元素
    
    * 命令：
        - **blpop key1[key2] timeout** 移除并获取列表的第一个元素，如果列表没有元素阻塞列表直到等待超时或者可以弹出元素为止
        
        - **brpop key1[key2] timeout** 移除并获取列表的最后一个元素，如果列表没有元素阻塞列表直到等待超时或者可以弹出元素为止
        
        - **brpoplpush source destination timeout** 从列表弹出一个值，将弹出的值插入到另一个列表中并返回他，如果列表中没有元素阻塞列表直到等待超时或者可以弹出元素为止
        
        - **lindex key index** 通过索引获取列表中的元素
        
        - **linsert key before|after pivot value** 在列表的元素之前后者之后插入元素
        
        - **llen key** 获取列表的长度
        
        - **lpop key** 移除列表中的第一个元素并返回它
        
        - **lpush key value1[value2]** 将一个或者多个元素插入到列表的头部
        
        - **lpusx key value** 将一个元素插入到已存在的列表中的头部
        
        - **lrange key start stop** 获取列表指定范围内的元素
        
        - **lrem key count value** 根据参数 COUNT 的值，移除列表中与参数 VALUE 相等的元素
        
            COUNT 的值可以是以下几种：
            
            - count > 0 : 从表头开始向表尾搜索，移除与 VALUE 相等的元素，数量为 COUNT
            
            - count < 0 : 从表尾开始向表头搜索，移除与 VALUE 相等的元素，数量为 COUNT 的绝对值
            
            - count = 0 : 移除表中所有与 VALUE 相等的值
            
        - **lset key index value** 通过索引设置列表元素的值
        
        - **ltrim key start stop** 对列表修剪，只保留指定区间内的值，不在指定区间内的元素将被删除
        
        - **rpop key** 移除列表中最后一个元素并返回它
        
        - **rpoplpush source destination** 移除列表中的最后一个元素，并将改元素添加到另一个列表中返回
        
        - **rpush key value1[value2]** 在列表的尾部添加一个或多个元素
        
        - **rpushx key value** 将一个元素插入到已存在的列表中的尾部

- ### Set
    * 可存储的值：无序集合
    
    * 操作：添加，获取，移除单个元素、判断一个元素是否存在集合中、计算交集，并集，差集、从集合中随机获取元素
    
    * 命令：
        - **sadd key member1[member2]** 想集合中添加一个或多个元素
        
        - **scard key** 获取集合的成员数
        
        - **sdiff key1[key2]** 返回指定集合的差集
        
        - **sdiffstore destination key1[key2]** 返回指定集合的差集并且存储到destination中
        
        - **sinter key1[key2]** 返回指定集合的交集
        
        - **sinterstore destination key1[key2]** 返回指定集合的交集并且存储到destination中
        
        - **sismember key member** 判断member元素是否存在集合key中
        
        - **smember key** 返回集合中的所有元素
        
        - **smove source destination member** 将member元素从集合source移动到集合destination中
        
        - **spop key** 移除并返回集合中的一个随机元素
        
        - **srandmember key [count]** 返回集合中一个或多个随机元素
        
        - **srem key member1[member2]** 移除集合中一个或多个元素
        
        - **sunion key1[key2]** 返回指定集合的并集
        
        - **sunionstore destinatin key1[key2]** 返回指定集合的并集并且存储到集合destination中
        
        - **sscan key cursor [match pattern][count count]** 迭代集合中的元素
          
- ### Hash
    * 可存储的值：包含键值对的无序散列表
    
    * 操作：添加，获取，移除单个键值对、获取所有的键值对、检查某个键是否存在
    
    * 命令：
        - **hdel key field1[field2]** 删除一个或多个哈希表字段
        
        - **hexists key field** 查看哈希表key中，field是否存在
        
        - **hget key field** 获取存储在哈希表中指定字段的值
        
        - **hgetall key** 获取哈希表中的所有字段和值
        
        - **hincrby key field increment** 为哈希表key指定字段的整数值增加increment
        
        - **hincrbyfloat key field increment** 为哈希表key执行字段的浮点数增加increment
        
        - **hkeys key** 获取哈希表key中所有字段
        
        - **hlen key** 获取哈希表中字段数量
        
        - **hmget key field1[field2]** 获取都有给定字段的值
        
        - **hmset key field1 value1[field2 value2]** 同时这是多个field-value对到哈希表key中
        
        - **hset key field value** 将哈希表key中的field的值设置为value
        
        - **hsetnx key field value** 只有字段field不存在时才设置哈希表字段的值

        - **hvals key** 获取哈希表中所有的值
        
        - **hscan key cursor[match pattern][count count]** 迭代哈希表的键值对
        
- ### Sorted Set
    * 可存储的值：有序集合
    
    * 操作：添加、获取、移除单个元素，根据分值范围或者成员获取元素，计算一个键的排名
    
    * 命令：
        - **zadd key score1 member1[score2 member2]** 向有序集合插入一个或多个成员，或者更新已存在成员的分数
        
        - **zcard key** 获取有序集合的成员个数
        
        - **zount key min max** 计算在有序集合中指定区间分数的成员数
        
        - **zincrby key increment member** 有序集合中对指定成员的分数增加increment
        
        - **zinterstore destination numkeys key[key...]** 计算给定一个或多个有序集合的交集并且将结果存储在新有序集合中
        
        - **zlencount key min max** 在有序集合中计算指定字典区间内成员的数量
        
        - **zrange key start stop[withscores]** 通过索引区间返回有序集合中指定区间内的成员
        
        - **zrangebylex key min max[limit offset count]** 通过字典区间返回有序集合的成员
        
        - **zrangebyscore key min max[withscore][limit]** 通过分数返回有序集合指定区间内的成员
        
        - **zrank key member** 返回有序集合指定成员的索引
        
        - **zrem key member[member...]** 移除有序集合中一个或多个成员
        
        - **zremrangebylex key min max** 移除有序集合中给定字典区间内的所有成员
        
        - **zremrangebyrank key start stop** 移除有序集合中给定排名区间内的所有成员
        
        - **zremrangebyscore key min max** 移除有序集合中给定分数区间内的所有成员
        
        - **zrevrange key start stop[withscores]** 返回有序集合中指定区间内的成员，通过索引，分数由高到低
        
        - **zrevrangebyscore key max min[withscores]** 返回有序集合中执行分数区间内的成员，分数由高到低
        
        - **zrevrank key member** 返回有序集合中指定成员的排名，有序集合成员按分数值递减排序
        
        - **zscore key member** 返回有序集合中成员的分数
        
        - **zunionstore destination numkeys key[key...]** 计算给定的一个或多个有序集合的并集，并且存储到新的key中
        
        - **zscan key cursor[match pattern][count count]** 迭代集合中的元素(包括元素成员和元素分数)
    - ### **pipeline** 
        批量执行多个命令，但是不是原子操作，服务器端会把命令拆分 ；并且只能作用在一个Redis节点上
        
# 三、发布订阅
- 如下图，三个客户端订阅了一个频道(channel):

<div align="center"><img src="resources/redis/subscirbe.png" width="400"/></div><br>

- 如下图，当有新的消息发布到channel时，这个消息就会被发送给订阅它的三个客户端

<div align="center"><img src="resources/redis/publish.png" width="400"/></div><br>

- 发布订阅的命令：

  - **psubscribe pattern[pattern...]** 订阅一个或多个符合给定模式的频道

  - **pubsub subcommand[argument[argument...]]** 查看订阅与发布系统状态

  - **publish channel message** 将信息发送到指定的频道上

  - **punsubscribe [pattern[pattern...]]** 退订所有给定模式的频道

  - **subscribe channel[channel...]** 订阅一个或者多个频道

  - **unsubscribe [channel[channel...]]** 退订给定的频道  

# 四、键的过期时间
- Redis可以为每个键设置过期时间，当键过期时，会自动删除此键

- 对于散列表(Hash)，只能为整个键设置过期时间(整个散列表),不能为键里面的单个元素设置过期时间

- 命令：
    - **expire key seconds** 将键key的过期时间设置为seconds秒

    - **pexire key millseconds** 将键key的过期时间这是为millseconds毫秒

    - **expireat key seconds[timestamp]** 将键key 的过期时间设置为timestamp所指定的秒数时间戳

    - **pexpireat key millseconds[timestamp]** 将键key 的过期时间设置为timestamp所指定的毫秒数时间戳

    - **setex key seconds value** 设置key的值为value，并且设置key的过期时间位senconds(秒),特定的数据类型String

    - **psetex key millseconds value** 设置key的值为value，并且设置key的过期时间位millseconds(毫秒)，特定的数据类型String

# 五、数据淘汰策略
- **volatile-lru** ： 从已设置过期时间的数据集中挑选最近最少使用的数据进行淘汰

- **volatile-ttl** ： 从已设置过期时间的数据集中挑选将要过期的数据进行淘汰

- **volatile-random** ： 从已设置过期时间的数据集中任意选择数据进行淘汰

- **allkeys-lru** ： 从所有数据集中挑选最近最少使用的数据进行淘汰

- **allkeys-random** ： 从素有数据集中任意选择数据进行淘汰

- **noeviction** ： 禁止驱逐数据

- Redis 4.0 引入了 volatile-lfu 和 allkeys-lfu 淘汰策略，LFU 策略通过统计访问频率，将访问频率最少的键值对淘汰。

# 六、持久化
- ### RDB持久化
    将某个时间点的数据全部放到硬盘上，可以将快照复制到其他服务器上从而创建具有相同数据的服务器副本，显而易见，如果系统发生故障，将会丢失最后一次创建快照之后的数据，如果数据较大，则保存快照的时间就会越长

    RDB实际上存放的是数据文件，恢复时直接将数据文件加载到内存中即可
- ### AOF持久化
    将写命令添加到AOF文件的末尾

    使用AOF持久化需要设置同步选项，指定写命令什么时候会同步到磁盘上，因为对文件进行写入并不会马上将内容同步到磁盘上，而是先存储到缓冲区，然后有操作系统决定什么时候同步到磁盘上

    - 同步选项：
        - **always** ： 每个命令都同步，会严重降低服务器的性能

        - **everysec** ： 每秒同步一次，比较合适，可以保障系统崩溃时只会丢失一秒左右的数据，并且Redis每秒执行一次同步服务对服务器性能几乎没有任何影响

        - **no** ： 让操作系统决定何时同步，其实并不能给服务器带来多大的性能提升，反而会增加系统崩溃时数据丢失的数量

    随着服务的请求数量增加，AOF文件会越来越大，Redis提供了一种AOF重写机制，能够去除AOF文件中的冗余写命令 

    AOF存放的是指令日志，做数据恢复时，其实是要回放和执行所有的指令日志 

# 七、事物
一个事物包含多个命令，服务器在执行事物期间，不会执行其他客户端的命令

事物中的多个命令是一起发送给服务器的，而不是一条一条的，这种方式成为流水线，它可以减少客户端与服务器之间的网络通讯测试从而提高性能。

事物的实现方式是使用**MULTI**和**EXEC**命令将事物包围起来的
# 八、事件
# 九、集群
Redis集群提供了一种方式自动将数据分布在多个Redis节点上面

- ### 主从复制 master-slave
    做到读写分离，一般master去写入数据，slave读取数据

- ### 集群TCP端口
    每个集群的Redis节点都需要打开两个TCP连接，一个连接用于给客户端提供服务，另一个用于集群总线(cluster bus)(集群总线用于节点的失败侦测、配置更新、故障转移授权等)，命令端口和集群总线端口的偏移总是1000，例如命令端口为6379，则集群总线端口为16379

- ### 集群数据切片
    Redis集群不同一致性哈希，它用一种不同的分片形式，在这种形式中，每个key都是一个概念性(hash slot)的一部分

    Redis集群中有16384个hash slot，数据库中的每个键都属于这16384个哈希槽的其中一个，集群使用公式CRC16(KEY) % 16384来计算键属于那个槽，CRC16(KEY)用于计算keyCRC16校验和

    Redis集群中的每个节点负责一部分hash slots，假设你的集群有3个节点，那么：

    - 节点 A 负责处理 0 号至 5500 号哈希槽。

    - 节点 B 负责处理 5501 号至 11000 号哈希槽。

    - 节点 C 负责处理 11001 号至 16384 号哈希槽。

    允许添加和删除集群节点。比如，如果你想增加一个新的节点D，那么久需要从A、B、C节点上删除一些hash slot给到D。同样地，如果你想从集群中删除节点A，那么会将A上面的hash slots移动到B和C，当节点A上是空的时候就可以将其从集群中完全删除。

    因为将hash slots从一个节点移动到另一个节点并不需要停止其它的操作，添加、删除节点以及更改节点所维护的hash slots的百分比都不需要任何停机时间。也就是说，移动hash slots是并行的，移动hash slots不会影响其它操作。

    Redis支持多个key操作，只要这些key在一个单个命令中执行（或者一个事务，或者Lua脚本执行），那么它们就属于相同的hash slot。你也可以用hash tags俩强制多个key都在相同的hash slot中。

- ### 集群主从模式
    当部分master节点失败了，或者不能够和大多数节点通信的时候，为了保持可用，Redis集群用一个master-slave模式，这样的话每个hash slot就有1到N个副本。

    在我们的例子中，集群有A、B、C三个节点，如果节点B失败了，那么5501-11000之间的hash slot将无法提供服务。然而，当我们给每个master节点添加一个slave节点以后，我们的集群最终会变成由A、B、C三个master节点和A1、B1、C1三个slave节点组成，这个时候如果B失败了，系统仍然可用。节点B1是B的副本，如果B失败了，集群会将B1提升为新的master，从而继续提供服务。然而，如果B和B1同时失败了，那么整个集群将不可用。

- ### 集群一致性保证
# 十、应用场景

- ### 计数器
    可以对String进行自增自减操作，从而实现计数器

    redis因为时内存性数据库读写性能非常高，很适合存储频繁读写的计数量

- ### 缓存
    将热点数据放到内存中，设置内存的最大使用量以及淘汰策略来保证缓存的命中率

    今后会对缓存做更详细的介绍

- ### 查找表
    例如DNS记录就很适合使用redis进行存储

    查找表和缓存类似，也是利用redis快速查找特性，但是查找表的内容不能失效，而缓存的内容可以失效，缓存不能作为可靠的数据源

- ### 消息多列
    List是一个双向链表，可以通过lpop和lpush写入和读取消息

    不过最好还是使用RabbitMQ等消息中间件吧

- ### 会话缓存
    使用redis存储多台应用服务器的会话信息

    当应用服务器不在存储用户的会话信息，也就不在具有状态，一个用户可以请求任意一个应用服务器，从而实现高可用性以及伸缩性

- ### 分布式锁
    利用setnx命令实现分布式锁

- ### 其他
    set可以实现交集、并集等操作，从而实现共同友好的功能

    zset可以实现有序性操作，从而实现排行榜等功能

	还原合并(docker部署):
	docker cp ef4:/opt/redis-4.0.10/bin/redis-cli /root
   ./redis-cli -h 192.168.6.26 -a Gepoint --pipe < appendonly.aof 

           