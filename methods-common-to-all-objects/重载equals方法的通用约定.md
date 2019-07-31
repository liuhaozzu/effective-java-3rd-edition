## 如果满足以下条件，不用重载
1. 一个类的每个实例都是唯一的  
2. 没必要提供“逻辑相等”的功能，比如java.util.regex.Pattern  
3. 父类已经重载了equals方法，且适合子类  
4. 对于packate-private的类，如果确信equals方法不会被调用，则可以不用重载

## 相等关系应该有的性质
1. 自反性，对于任何非null值，x.equals(x)返回true  
2. 对称性，对于任何非null值，x.equals(y),必有y.equals(x)  
3. 传递性  
4. 一致性  
5. 对任何非null值x,x.equals(null)必返回false

## 写出高质量equals方法的建议
1. 使用==检测是否为同一个引用
2. 使用instanceof 关键字检测类型是否正确
3. 将被比较对象强转为比较对象。
4. 对于对象中每一个“有意义”的属性，逐一检测两者是否匹配
5. 重新检测你所写的equals方法是否满足上面的性质

## 重载equals的同时，一定要重载hashCode方法
## 不要改名equals的方法签名中的参数类型
