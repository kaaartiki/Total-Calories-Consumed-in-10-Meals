# Total-Calories-Consumed-in-10-Meals
    #include <stdio.h>

    int totalCalories(int *calories, int n) {
    if (n == 0)
        return 0;
    else
        return *calories + totalCalories(calories + 1, n - 1);
    }

    int maxCalories(int *calories, int n) {
    if (n == 1)
        return *calories;
    int maxRest = maxCalories(calories + 1, n - 1);
    return (*calories > maxRest) ? *calories : maxRest;
    }

    int minCalories(int *calories, int n) {
    if (n == 1)
        return *calories;
    int minRest = minCalories(calories + 1, n - 1);
    return (*calories < minRest) ? *calories : minRest;
    }

    int main() {
    int calories[10] = {250, 300, 200, 400, 150, 350, 300, 250, 200, 400};
    int threshold = 300;  // for counting high-calorie meals

    printf("Calories for 10 meals:\n");
    for (int i = 0; i < 10; i++)
        printf("Meal %d: %d\n", i + 1, calories[i]);

    int total = totalCalories(calories, 10);
    float average = (float)total / 10;
    int max = maxCalories(calories, 10);
    int min = minCalories(calories, 10);

    int above = 0, below = 0;
    for (int i = 0; i < 10; i++) {
        if (calories[i] > threshold)
            above++;
        else
            below++;
    }

    printf("\n--- Summary ---\n");
    printf("Total calories consumed: %d\n", total);
    printf("Average calories per meal: %.2f\n", average);
    printf("Highest calorie meal: %d\n", max);
    printf("Lowest calorie meal: %d\n", min);
    printf("Meals above %d calories: %d\n", threshold, above);
    printf("Meals below or equal %d calories: %d\n", threshold, below);

    return 0;
    }
