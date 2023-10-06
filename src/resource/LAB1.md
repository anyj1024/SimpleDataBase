LAB 1

Lab 1-1  
主要实现了Tuple和TupleDesc两个类  
Tuple 表示表中的一行记录(row),它包含了这一行数据的实际值.   
TupleDesc 描述这些记录的结构(schema),它包含字段名称、类型等元信息.   
数据库中，行被称为记录(record)或元组(tuple),列称为字段(field)或属性(attribute)。tuples在SimpleDB中十分基础，是一组Field对象的集合，Field是不同数据类型(e.g.,integer,string)实现的接口，Tuple对象是由底层访问方法(e.g.,heap files,B trees)创建的，Tuple也有类型type（或称为组织结构schema），称为_tuple descriptor_，是TypleDesc对象，这个对象包括了Type对象的集合。


Lab 1-2  
主要实现了Catalog类


Lab1-3  
主要实现了BufferPool类