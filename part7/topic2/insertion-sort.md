# Insertion Sort

* Sorts input numbers **_in place_**, i.e. it arranges the numbers within the array A, with at most a constant number of them stored outside the array at any time.
* Modifies the original array.
* Time Complexity is O(n^2)

## Code
```java
    public void sort(int[] numbers) {
        for(int i = 1; i < numbers.length; i++) {
            int tmp = numbers[i];
            int j = i;

            while(j > 0 && numbers[j - 1] >= tmp) {
                numbers[j] = numbers[j - 1];
                j--;
            }
            numbers[j] = tmp;
        }
    }
```