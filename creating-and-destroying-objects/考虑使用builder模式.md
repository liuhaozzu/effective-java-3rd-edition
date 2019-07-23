## 当面临许多参数时，建议使用builder模式
1. 可伸缩的构造函数易用性较差，且不易读。
    ```
    public class NutritionFacts {
        private final int servingSize;
        private final int servings;
        private final int calories;
        private final int fat;
        private final int sodium;
        private final int carbohydrate;

        public NutritionFacts(int servingSize, int servings) {
            this(servingSize, servings, 0);
        }
        
        public NutritionFacts(int servingSize, int servings, int calories) {
            this(servingSize, servings, calories, 0);
        }

        public NutritionFacts(int servingSize, int servings, int calories, int fat) {
            this(servingSize, servings, calories, fat, 0);
        }

        public NutritionFacts(int servingSize, int servings, int calories, int fat, int sodium) {
            this(servingSize, servings, calories, fat, sodium, 0);
        }
        
        public NutritionFacts(int servingSize, int servings, int calories, int fat, int sodium, int carbohydrate) {
            this.servingSize = servingSize;
            this.servings = servings;
            this.calories = calories;
            this.fat = fat;
            this.sodium = sodium;
            this.carbohydrate = carbohydrate;
        }
    }
    ```
2. JavaBeans pattern：
  ```
  NutritionFacts cocaCola = new NutritionFacts();
  cocaCola.setServingSize(240);
  cocaCola.setServings(8);
  ...
  ```
3. Builder 模式
  ```
  public class NutritionFactsBuilderPattern {
    private int servingSize;
    private int servings;
    private int calories;
    private int fat;
    private int sodium;
    private int carbohydrate;

    public NutritionFactsBuilderPattern(Builder builder) {
        servingSize = builder.servingSize;
        servings = builder.servings;
        calories=builder.calories;
        fat = builder.fat;
        sodium = builder.sodium;
        carbohydrate = builder.carbohydrate;
    }

    public static class Builder {
        //required params
        private final int servingSize;
        private final int servings;

        //optional params
        private int calories=0;
        private int fat=0;
        private int sodium=0;
        private int carbohydrate = 0;

        public Builder(int servingSize, int servings) {
            this.servingSize = servingSize;
            this.servings = servings;
        }
        public Builder calories(int calories) {
            this.calories = calories;
            return this;
        }
        public Builder fat(int fat) {
            this.fat = fat;
            return this;
        }
        public Builder sodium(int sodium) {
            this.sodium = sodium;
            return this;
        }
        public Builder carbohydrate(int carbohydrate) {
            this.carbohydrate = carbohydrate;
            return this;
        }
        public NutritionFactsBuilderPattern build() {
            return new NutritionFactsBuilderPattern(this);
        }
    }
}
  ```
3.1 builder模式有利于构建类继承关系
```
public class Pizza {
    public enum Topping {HAM,MUSHROOM,ONION,PEPPER, SAUSAGE}
    final Set<Topping> toppings;
    abstract static class Builder<T extends Builder<T>> {
        EnumSet<Topping> toppings = EnumSet.noneOf(Topping.class);
        public T addTopping(Topping topping) {
            toppings.add(Objects.requireNonNull(topping));
            return self();
        }
        abstract Pizza build();
        protected abstract T self();
    }

    Pizza(Builder<?> builder) {
        toppings = builder.toppings.clone();
    }
}

public class NyPizza extends Pizza {
    public enum Size {SMALL, MEDIUM, LARGE,}
    private final Size size;
    public static class Builder extends Pizza.Builder<Builder> {
        private final Size size;
        public Builder(Size size) {
            this.size = Objects.requireNonNull(size);
        }
        @Override
        Pizza build() {
            return new NyPizza(this);
        }
        @Override
        protected Builder self() {
            return this;
        }
    }
    NyPizza(Builder builder) {
        super(builder);
        size = builder.size;
    }
}
```
