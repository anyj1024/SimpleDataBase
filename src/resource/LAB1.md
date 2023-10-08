LAB 1

Lab 1-1  
主要实现了Tuple和TupleDesc两个类  
Tuple 表示表中的一行记录(row),它包含了这一行数据的实际值.   
TupleDesc 描述这些记录的结构(schema),它包含字段名称、类型等元信息.   
数据库中，行被称为记录(record)或元组(tuple),列称为字段(field)或属性(attribute)。tuples在SimpleDB中十分基础，是一组Field对象的集合，Field是不同数据类型(e.g.,integer,string)实现的接口，Tuple对象是由底层访问方法(e.g.,heap files,B trees)创建的，Tuple也有类型type（或称为组织结构schema），称为_tuple descriptor_，是TypleDesc对象，这个对象包括了Type对象的集合。


Lab 1-2  
主要实现了Catalog类  
主要是一个key为Integer,value为Table的并发集合,Table类主要有DbFile/TableName/PrimaryKey属性.  
catalog类描述的是数据库实例。包含了数据库现有的表信息以及表的schema信息。现在需要实现添加新表的功能，以及从特定的表中提取信息。提取信息时通过表对应的TupleDesc对象决定操作的字段类型和数量.  
全局catalog是分配给整个SimpleDB进程的Catalog类一个实例，可以通过方法Database.getCatalog()获得，global buffer pool可以通过方法Database.getBufferPool()获得.


Lab1-3  
主要实现了BufferPool类  
buffer pool（在SimpleDB中是BufferPool类）负责将内存最近读过的物理页缓存下来。所有的读写操作通过buffer pool读写硬盘上不同文件，BufferPool里的numPages参数确定了读取的固定页数，在之后的lab中，需要实现淘汰机制(eviction policy)。在这个lab中，只需要实现构造器和BufferPool.getPage()方法，BufferPool应该存取最多numPages个物理页，当前lab中如果页的数量超过numPages，先不实现eviction policy，先扔出一个DbException错误。  
Database类提供了一个静态方法Database.getBufferPool()，返回整个SimpleDB进程的BufferPool实例引用。

lab1-4
主要实现了HeapPageId、RecordId和HeapPage三个类  
硬盘中包含很多文件，其中有的文件就是我们的HeapFile，一个HeapFile中存储了我们这个数据库中的所有表。文件由硬盘中的许多页(Page)构成，在我们的实现中，每个Page存储一个Table，当Page被加载到内存中后它就是一个表的形式。而每个页又包含很多slot，一个slot里有一个tuple。  
一个HeapFile对象被安排成一组页面，每个页面由固定数量的字节组成，用于存储 tuple ，（由常数BufferPool.DEFAULT_PAGE_SIZE定义），包括一个头。在SimpleDB中，数据库中每个表都有一个HeapFile对象。HeapFile中的每个页面被安排为一组槽，每个槽可以容纳一个元组（SimpleDB中一个给定的表的元组都是相同大小的）。除了这些槽之外，每个页面都有一个头，由一个位图组成，每个元组槽有一个位。如果某个元组对应的位是1，表示该元组是有效的；如果是0，表示该元组是无效的（例如，已经被删除或者从未被初始化）。 HeapFile对象的页是HeapPage类型，实现了Page接口。页被存储在缓冲池中，但由HeapFile类来读写。
