## 公有的静态成员变量
```
public class Elvis {
    public static final Elvis INSTANCE = new Elvis();
    ...
}
```

## 静态工厂方法
```
public class Elvis {
    private static final Elvis INSTANCE = new Elvis();
    private Elvis() {}
    public static Elvis getInstance() {
        return INSTANCE;
    }
    //防止反序列化生成实例
    private Object readResolve() {
        return INSTANCE;
    }
}
```

## 声明一个单元素的枚举
```
public enum  ElivsEnum {
    INSTANCE;
    
    ...
}
```
