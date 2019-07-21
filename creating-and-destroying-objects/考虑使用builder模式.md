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
