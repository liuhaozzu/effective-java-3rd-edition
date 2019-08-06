## 推荐使用泛型类型代替Object
1. 数组中的元素只能是具体类型
2. 泛型类中使用数组时，通常有两种方式  
  2.1 强制转型
      ```
      E[] elements = (E[]) new Object[2];
      ```
  2.2 将数组声明成Object[],获取元素时，再强转成E
      ```
      Object[] elements = new Object[2];
      E element = (E) elements[0];
      ```
 ## 推荐使用泛型方法
 1. 
