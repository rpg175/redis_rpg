# Redis的数据结构

## 链表
* 双端：链表节点带有prev和next指针，获取某个节点的前置节点和后置节点的复杂度都是O（1）。 
* 无环：表头节点的prev指针和表尾节点的next指针都指向NULL，对链表的访问以NULL为终点。 
* 带表头指针和表尾指针：通过list结构的head指针和tail指针，程序获取链表的表头节点和表尾节点的复杂度为O（1）。 
* 带链表长度计数器：程序使用list结构的len属性来对list持有的链表节点进行计数，程序获取链表中节点数量的复杂度为O（1）。 
* 多态：链表节点使用void*指针来保存节点值，并且可以通过list结构的dup、free、match三个属性为节点值设置类型特定函数，所以链表可以用于保存各种不同类型的值

## 字典
* 字典被广泛用于实现Redis的各种功能，其中包括数据库和哈希键。 
* Redis中的字典使用哈希表作为底层实现，每个字典带有两个哈希表，一个平时使用，另一个仅在进行rehash时使用。
* 当字典被用作数据库的底层实现，或者哈希键的底层实现时，Redis使用MurmurHash2算法来计算键的哈希值。 
* 哈希表使用链地址法来解决键冲突，被分配到同一个索引上的多个键值对会连接成一个单向链表。 
* 在对哈希表进行扩展或者收缩操作时，程序需要将现有哈希表包含的所有键值对rehash到新哈希表里面，并且这个rehash过程并不是一次性地完成的，而是渐进式地完成的


## 补一些epoll原理
问题：
用c写 epoll 监听 accept事件，也就是epollin，然后唤醒后调用accept函数拿到socket的地址

做完了，然后用  主机浏览器或者shell调用curl函数测试