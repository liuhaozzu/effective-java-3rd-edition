## stream pipeline是延迟求值的
1. 在最终的Action操作被调用之前，求值不会开始
2. 完成最终的Action运算不需要的数据不会被计算。
3. lambdas表达式本身也是延迟求值的
  ```
  public Long getLong(Map map, Object key, Function<Object, Long> function) {
      Long value = MapUtils.getLong(map, key);
      if (value == null) {
          return function.apply(key);
      } else {
          return value;
      }
  }
  
  Map<String, String> map = new HashMap<>();
  MapUtils2 mapUtils2 = new MapUtils2();
  map.put("abc", "123");
  long abc = mapUtils2.getLong(map, "abc", (abc2)->{
      //该lambdas表达式将会延迟求值
      System.out.println("getLong");
      return System.currentTimeMillis();
  });
  
  ```

## 过犹不及
1. 过度使用stream会使代码的可读性和易维护性降低
2. 由于没有显式类型，lambdas参数的 命名对代码的可读性至关重要

## stream和传统代码块的的对比
1. 在传统代码块中，可以修改任意本地变量；在lambdas中只能读取final或effective final的变量，并且不能修改这些变量
2. 在传统代码块中，可以通过return，continue，break跳出循环；在lambdas中不可以

## 适合使用stream的场景
1. 统一的转换序列
2. 过滤
3. 组合元素
4. 累积元素进集合中
5. 集合中搜索元素

## 推荐使用没有副作用的函数

## stream计算的返回值最好是Collection，而不是Stream。

## 慎用parallel
1. 当source是Stream.iterate 或者 中间有limit操作时，使用parallel不太可能增加性能
2. 当source是ArrayList,HashMap,HashSet,ConcurrentHashMap实例，或者数组，int range,long range时，parallel可以获得较好的性能
3. parall不但会降低性能，还会造成不正确的结果和不可预期的行为。
4. ***在合适的场景下，parallel可以获得跟cpu核数成线性的加速***
  4.1 Prime-counting
      ```
      long count = LongStream.rangeClosed(2, 1000000)
                //can accelerate the calculation
                .parallel()
                .mapToObj(BigInteger::valueOf)
                .filter(i -> i.isProbablePrime(50))
                .count();
      ```
