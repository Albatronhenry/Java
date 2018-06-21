[ArrayList & LinkedList]()

ArrayList和LinkedList的区别有以下几点：

        1. ArrayList是实现了基于动态数组的数据结构，而LinkedList是基于链表的数据结构；

        2. 对于随机访问get和set，ArrayList要优于LinkedList，因为LinkedList要移动指针；

        3. 对于添加和删除操作add和remove，一般大家都会说LinkedList要比ArrayList快，因为ArrayList要移动数据。
        
ArrayList是使用数组实现的,若要从数组中删除或插入某一个对象，需要移动后段的数组元素，从而会重新调整索引顺序,调整索引顺序会消耗一定的时间，所以速度上就会
比LinkedList要慢许多. 相反,LinkedList是使用链表实现的,若要从链表中删除或插入某一个对象,只需要改变前后对象的引用即可!

[存储结构参考](https://github.com/Albatronhenry/DataStructure/blob/master/%E5%AD%98%E5%82%A8%E7%BB%93%E6%9E%84.md)
