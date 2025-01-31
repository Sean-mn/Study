# 쉘 정렬

1. 이해

   Shell sort는 일정한 interval(간격)을 두고 떨어진 요소들끼리 부분집합을 만들어 insertion sort를 수행하는 것이다. insertion sort은 거의 정렬된 요소들에 대해서는 매우 빠른 속도를 보이기 때문에 이를 응용하여 효율을 높이는 것이다.

   1. interval을 정하고, interval 만큼 떨어진 요소들끼리 부분집합을 만든다.

   2. 부분집합에 대해 insertion sort를 수행한다.

   3. interval을 1이 될 때까지 $1/2$씩 줄여가며 반복한다.

   일반적으로 shell sort의 시간복잡도는 interval에 따라 달라지기는 하지만, $O(n^{1.25})$라고 한다.

2. 구현

   Shell sort의 기반이 insertion sort이기 때문에, 이를 먼저 구현해야 한다.

   ```c
    void insertionSort(int array[], int begin, int end, int interval) {
        for(int i = begin + interval; i <= end; i++) {
            int item = array[i];
            for (int j = i - interval; j >= begin && array[j] > item; j = j - interval) {
                array[j + interval] = array[j];
            }
            array[j + interval] = item;
        }
    }
   ```

   주어진 interval만큼 떨어진 요소들끼리 부분집합을 만들어 insertion sort를 수행한다.

   실질적인 shell sort의 구현은 다음과 같다.

   ```c
    void shellSort(int array[], int length) {
        int interval = length / 2;
        while (interval >= 1) {
            for(int i = 0; i < interval; i++) {
                insertionSort(array, i, length-1, interval);
            }
            interval = interval / 2;
        }
    }
   ```

   위 코드에서는 array 길이의 절반으로 interval을 초기화하고, interval이 1이 될 때까지 반복하게끔 되어 있다. 그 안에서 모든 부분집합에 대해 `insertionSort()`를 수행하는 것을 볼 수 있다.

---
