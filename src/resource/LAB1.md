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
