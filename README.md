# Searching

time               | best      | worst
-------------------|-----------|-------
linear search      | O(1)      | O(n)
binary search      | O(log n)  | O(log n)
ternary search     | O(log3 n) | O(log3 n)
jump search        | O(sqrt n) | O(sqrt n)
exponential search | O(log i)  |

### Linear Search
![](https://github.com/shamy1st/algorithms/blob/main/images/linear-search.png)

--             | best   | worst
---------------|--------|-------
linear search  | O(1)   | O(n)

        public int linearSearch(T[] array, T value) {
            for(int i=0;i<array.length;i++)
                if(array[i].compareTo(value) == 0)
                    return i;

            return -1;
        }

### Binary Search
![](https://github.com/shamy1st/algorithms/blob/main/images/binary-search.png)

--             | time     
---------------|----------
binary search  | O(log n) 

space          | interative | recursive
---------------|------------|----------
binary search  | O(1)       | O(log n)

log 1000,000 = 19

* **Recursive**

        public int binarySearchRecursive(T[] array, T value) {
            return binarySearchRecursive(array, value, 0, array.length - 1);
        }

        private int binarySearchRecursive(T[] array, T value, int start, int end) {
            if(start > end)
                return -1;

            int middle = (start + end) / 2;
            if(value.compareTo(array[middle]) == 0)
                return middle;
            else if(value.compareTo(array[middle]) < 0)
                return binarySearchRecursive(array, value, start, middle - 1);
            return binarySearchRecursive(array, value, middle + 1, end);
        }

* **Iterative**

        public int binarySearchIterative(T[] array, T value) {
            int start = 0;
            int end = array.length - 1;

            while(start <= end) {
                int middle = (start + end) / 2;
                if(value.compareTo(array[middle]) == 0)
                    return middle;
                else if(value.compareTo(array[middle]) < 0)
                    end = middle - 1;
                else
                    start = middle + 1;
            }
            return -1;
        }

### Ternary Search
![](https://github.com/shamy1st/algorithms/blob/main/images/ternary-search.png)
![](https://github.com/shamy1st/algorithms/blob/main/images/ternary-search-2.png)
![](https://github.com/shamy1st/algorithms/blob/main/images/binary-vs-ternary.png)

--             | time     
---------------|----------
ternary search | O(log3 n) 

* **Hint**: binary search is faster than ternary search

        public int ternarySearch(T[] array, T value) {
            return ternarySearch(array, value, 0, array.length - 1);
        }

        private int ternarySearch(T[] array, T value, int start, int end) {
            if(start > end)
                return -1;

            int partitionSize = (end - start) / 3;
            int mid1 = start + partitionSize;
            int mid2 = end - partitionSize;

            if(value.compareTo(array[mid1]) == 0)
                return mid1;

            if(value.compareTo(array[mid2]) == 0)
                return mid2;

            if(value.compareTo(array[mid1]) < 0)
                return ternarySearch(array, value, start, mid1 - 1);
            else if(value.compareTo(array[mid1]) > 0 && value.compareTo(array[mid2]) < 0)
                return ternarySearch(array, value, mid1 + 1, mid2 - 1);
            return ternarySearch(array, value, mid2 + 1, end);
        }

### Jump Search
![](https://github.com/shamy1st/algorithms/blob/main/images/jump-search.png)
![](https://github.com/shamy1st/algorithms/blob/main/images/jump-search-2.png)
![](https://github.com/shamy1st/algorithms/blob/main/images/jump-search-complexity.png)

--             | time     
---------------|----------
jump search    | O(sqrt n) 

        public int jumpSearch(T[] array, T value) {
            int blockSize = (int) Math.sqrt(array.length);
            int start = 0;
            int next = blockSize;

            while(start < array.length && array[next - 1].compareTo(value) < 0) {
                start = next;
                next += blockSize;
                if(next > array.length)
                    next = array.length;
            }

            for(int i=start;i<next;i++)
                if(value.compareTo(array[i]) == 0)
                    return i;

            return -1;
        }

### Exponential Search
![](https://github.com/shamy1st/algorithms/blob/main/images/exponential-search.png)
![](https://github.com/shamy1st/algorithms/blob/main/images/exponential-search-2.png)
![](https://github.com/shamy1st/algorithms/blob/main/images/exponential-search-3.png)
![](https://github.com/shamy1st/algorithms/blob/main/images/exponential-search-4.png)
![](https://github.com/shamy1st/algorithms/blob/main/images/exponential-search-complexity.png)

--                 | time     
-------------------|----------
exponential search | O(log i) 

        public int exponentialSearch(T[] array, T value) {
            int bound = 1;
            while(bound < array.length && array[bound].compareTo(value) < 0)
                bound *= 2;

            int start = bound / 2;
            int end = Math.min(bound, array.length - 1);
            return binarySearchRecursive(array, value, start, end);
        }
