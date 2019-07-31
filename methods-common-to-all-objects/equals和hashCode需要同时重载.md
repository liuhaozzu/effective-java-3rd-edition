## 必须同时重载equals和hashCode
### 约定
1. 同一个对象的hashCode方法必须一直返回同一值，假如equals方法中的比较字段的属性没有变化
2. 如果两个对象通过equals判断为相等，则hashCode值必须一致
3. 如果两个对象通过equals判断不相等，则hashCode不一定不一致。
### 计算hashCode时，不要因为性能而丢弃有意义的字段。
