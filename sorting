import time
import random
import sys
import matplotlib.pyplot as plt

sys.setrecursionlimit(2000000)

def merge_sort(arr):
    if len(arr) <= 1:
        return arr
    mid = len(arr) // 2
    left = merge_sort(arr[:mid])
    right = merge_sort(arr[mid:])
    return merge(left, right)

def merge(left, right):
    result = []
    i = j = 0
    while i < len(left) and j < len(right):
        if left[i] < right[j]:
            result.append(left[i])
            i += 1
        else:
            result.append(right[j])
            j += 1
    result.extend(left[i:])
    result.extend(right[j:])
    return result

def quick_sort_inplace(arr, low, high):
    if low < high:
        pi = partition(arr, low, high)
        quick_sort_inplace(arr, low, pi - 1)
        quick_sort_inplace(arr, pi + 1, high)

def partition(arr, low, high):
    pivot = arr[high]
    i = low - 1
    for j in range(low, high):
        if arr[j] <= pivot:
            i += 1
            arr[i], arr[j] = arr[j], arr[i]
    arr[i + 1], arr[high] = arr[high], arr[i + 1]
    return i + 1

def quick_sort(arr):
    A = arr.copy()
    quick_sort_inplace(A, 0, len(A) - 1)
    return A

def run_tests():
    test_cases = {
        "Empty": [],
        "One Element": [42],
        "Duplicates": [5, 2, 9, 5, 2, 3, 5],
        "Sorted": [1, 2, 3, 4, 5, 6, 7],
        "Reversed": [7, 6, 5, 4, 3, 2, 1]
    }
    
    print("=" * 50)
    print("TEST RESULTS:")
    print("=" * 50)
    for name, arr in test_cases.items():
        m_sorted = merge_sort(arr.copy())
        q_sorted = quick_sort(arr.copy())
        print(f"Case ({name}):")
        print(f"  Input:     {arr}")
        print(f"  MergeSort: {m_sorted}")
        print(f"  QuickSort: {q_sorted}
")

def measure_and_plot():
    sizes = [1000, 2000, 5000, 10000]
    
    merge_times_rand = []
    quick_times_rand = []
    
    for n in sizes:
        rand_data = [random.randint(0, 100000) for _ in range(n)]
        
        t0 = time.time()
        merge_sort(rand_data.copy())
        merge_times_rand.append(time.time() - t0)
        
        t0 = time.time()
        quick_sort(rand_data.copy())
        quick_times_rand.append(time.time() - t0)
        
    plt.figure(figsize=(10, 5))
    plt.plot(sizes, merge_times_rand, marker='o', label='Merge Sort O(n log n)')
    plt.plot(sizes, quick_times_rand, marker='s', label='Quick Sort (Last Pivot)')
    plt.title('Sorting Algorithm Performance (Random Data)')
    plt.xlabel('Array Size (n)')
    plt.ylabel('Execution Time (seconds)')
    plt.grid(True)
    plt.legend()
    plt.savefig('sorting_benchmark.png')
    print("Plot saved as sorting_benchmark.png")

if __name__ == "__main__":
    run_tests()
    measure_and_plot()
