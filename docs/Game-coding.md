# 游戏编码（Game Coding）
游戏编码涉及到了游戏常用的编程语言以及数据结构和算法，和一些应用于游戏特定场景的算法。

## 编程范式
### 指令式
### 过程式
### 函数式
### 面向对象
## 编程语言
### C++

### C#
#### 面向对象
#### 委托与事件
回调：通过使用委托，可以将一个方法作为参数传递给另一个方法，并在需要时调用该方法，从而实现回调功能。  
事件处理程序：委托常常用于定义事件处理程序。在C#中，事件是一种特殊的委托类型，用于响应用户操作或系统事件。  
多播委托：多播委托是一种允许将多个委托组合成一个委托的技术。通过多播委托，可以将多个方法绑定到同一个委托上，从而在触发委托时调用所有绑定的方法。  
增强代码的灵活性：委托使得代码更加灵活和可重用，因为它可以在运行时动态地绑定和解除方法。
### Lua

## 数据结构
### 栈
### 队列
### 数组
### 链表
### 树
### 图
### 堆
### 散列表

## 算法
### 查找
### 排序
#### 冒泡排序 O(n^2)
```csharp
static void bubbleSort(int[] nums){
    int t;
    bool sorted = false;
    for(int i = 0; i < nums.Length - 1; i++){
        sorted = true;
        for(int j = 0; j < num.Length - 1 - i; j++){
            if(nums[j] > nums[j + 1]){
                t = nums[j];
                nums[j] = nums[j + 1];
                nums[j + 1] = t;
                sorted = false;
            }
        }
        if(sorted) return;
    }
}
```
```cpp
void bubbleSort(int arr[], int n) {
    // 标记变量，表示本轮排序是否有交换操作
    bool sorted = false;
    for (int i = 0; i < n - 1 && !sorted; i++) {
        sorted = true;
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                // 交换元素
                swap(arr[j], arr[j + 1]);
                sorted = false;
            }
        }
    }
}
```
```lua
local function bubbleSort(arr)
    for i = 1, #arr, 1 do
        for j = 1, #arr - i, 1 do
            if arr[j] > arr[j+1] then
                arr[j], arr[j+1] = arr[j+1], arr[j]
            end
        end
    end
end
```
#### 插入排序 O(n^2)
```csharp
```
#### 选择排序 O(n^2)
```csharp
```
#### 快速排序 O(nlogn)
##### 递归版本
```cpp
void Vector<T>::quickSort ( Rank lo, Rank hi){
    if( hi - lo < 2 ) return;
    Rank mi = partition(lo, hi-1);
    quickSort(lo, mi);
    quickSort(mi + 1, hi);
}
Rank Vector<T>::partition( Rank lo, Rank hi){
    swap(_elem[lo], _elem[lo + rand() % (hi - lo + 1)]);
    T pivot = _elem[lo];
    while(lo < hi){
        while(lo < hi && pivot <= _elem[hi])
            hi--;
        _elem[lo] = _elem[hi];
        while(lo < hi && _elem[lo] <= pivot)
            lo++;
        _elem[hi] = _elem[lo];
    }
    _elem[lo] = pivot;
    return lo;
}
```
```csharp
using System;
using System.Collections.Generic;

public static class QuickSort {
    // 双向扫描法将数组划分成小于等于枢轴元素和大于枢轴元素两部分
    private static int Partition(List<int> nums, int left, int right) {
        int pivot = nums[(left + right) / 2]; // 选择中间元素作为枢轴元素
        while (left <= right) {
            while (nums[left] < pivot) left++;
            while (nums[right] > pivot) right--;
            if (left <= right) { // 左右指针未交错时交换元素
                int temp = nums[left];
                nums[left] = nums[right];
                nums[right] = temp;
                left++;
                right--;
            }
        }
        return left;
    }

    // 插入排序，用于对小规模子数组进行排序
    private static void InsertionSort(List<int> nums, int left, int right) {
        for (int i = left + 1; i <= right; i++) {
            int temp = nums[i];
            int j = i - 1;
            while (j >= left && nums[j] > temp) {
                nums[j + 1] = nums[j];
                j--;
            }
            nums[j + 1] = temp;
        }
    }

    // 快速排序递归函数
    private static void QuickSortRecursive(List<int> nums, int left, int right) {
        if (right - left + 1 <= 10) { // 对小规模子数组采用插入排序
            InsertionSort(nums, left, right);
            return;
        }
        int index = Partition(nums, left, right); // 双向扫描法将数组划分
        if (left < index - 1) {
            QuickSortRecursive(nums, left, index - 1); // 递归排序左半部分
        }
        if (index < right) {
            QuickSortRecursive(nums, index, right); // 递归排序右半部分
        }
    }

    // 快速排序函数
    public static void QuickSort(List<int> nums) {
        if (nums == null || nums.Count == 0) return;
        QuickSortRecursive(nums, 0, nums.Count - 1);
    }
}

// 测试代码
public static class Test {
    public static void Main() {
        List<int> nums = new List<int> {3, 2, 5, 1, 4};
        QuickSort.QuickSort(nums);
        foreach (int num in nums) {
            Console.Write(num + " ");
        }
        Console.WriteLine(); // 输出：1 2 3 4 5
    }
}
```
```cpp
#include <iostream>
#include <vector>

using namespace std;

// 双向扫描法将数组划分成小于等于枢轴元素和大于枢轴元素两部分
int partition(vector<int>& nums, int left, int right) {
    int pivot = nums[(left + right) / 2]; // 选择中间元素作为枢轴元素
    while (left <= right) {
        while (nums[left] < pivot) left++;
        while (nums[right] > pivot) right--;
        if (left <= right) { // 左右指针未交错时交换元素
            swap(nums[left], nums[right]);
            left++;
            right--;
        }
    }
    return left;
}

// 插入排序，用于对小规模子数组进行排序
void insertionSort(vector<int>& nums, int left, int right) {
    for (int i = left + 1; i <= right; i++) {
        int temp = nums[i];
        int j = i - 1;
        while (j >= left && nums[j] > temp) {
            nums[j + 1] = nums[j];
            j--;
        }
        nums[j + 1] = temp;
    }
}

// 快速排序递归函数
void quickSortRecursive(vector<int>& nums, int left, int right) {
    if (right - left + 1 <= 10) { // 对小规模子数组采用插入排序
        insertionSortRecursive(nums, left, right);
        return;
    }
    int index = partition(nums, left, right); // 双向扫描法将数组划分
    if (left < index - 1) {
        quickSortRecursive(nums, left, index - 1); // 递归排序左半部分
    }
    if (index < right) {
        quickSortRecursive(nums, index, right); // 递归排序右半部分
    }
}

// 快速排序函数
void quickSort(vector<int>& nums) {
    if (nums.empty()) return;
    quickSortRecursive(nums, 0, nums.size() - 1);
}

// 测试代码
int main() {
    vector<int> nums = {3, 2, 5, 1, 4};
    quickSort(nums);
    for (int num : nums) {
        cout << num << " ";
    }
    cout << endl; // 输出：1 2 3 4 5
    r
```
##### 非递归
快速排序的非递归版本是通过使用栈或队列来模拟递归过程实现的。与递归版本相比，它可以节省函数调用和维护函数调用栈所需的额外空间，因而在某些场景下可能具有更好的性能。  
由于递归的本质是函数调用，每次函数调用都会涉及到一定的时间开销，因此非递归版本可能具有更好的时间性能。与递归版本相比，非递归版本不需要保存过多的函数调用栈信息，因此可以节省一定的空间，但是代码可能更加复杂，可读性和可维护性也可能较差。
在下面的代码中，我们使用了一个 stack 类型的栈来模拟递归调用。首先将整个数组的下标范围 {0, nums.size()-1} 压入栈中，然后不断从栈顶取出一个待排序区间，执行双向扫描法进行划分，并将划分出的左右子区间（如果有）压入栈中，直到栈为空为止。  
```cpp
#include <iostream>
#include <vector>
#include <stack>

using namespace std;

// 双向扫描法将数组划分成小于等于枢轴元素和大于枢轴元素两部分
int partition(vector<int>& nums, int left, int right) {
    int pivot = nums[(left + right) / 2]; // 选择中间元素作为枢轴元素
    while (left <= right) {
        while (nums[left] < pivot) left++;
        while (nums[right] > pivot) right--;
        if (left <= right) { // 左右指针未交错时交换元素
            swap(nums[left], nums[right]);
            left++;
            right--;
        }
    }
    return left;
}

// 快速排序非递归函数
void quickSort(vector<int>& nums) {
    if (nums.empty()) return;
    stack<pair<int, int>> stk; // 使用栈模拟递归调用
    stk.push({0, nums.size() - 1});
    while (!stk.empty()) {
        int left = stk.top().first;
        int right = stk.top().second;
        stk.pop();
        if (left >= right) continue;
        int index = partition(nums, left, right); // 双向扫描法将数组划分
        stk.push({left, index - 1}); // 将左半部分压入栈中
        stk.push({index, right}); // 将右半部分压入栈中
    }
}

// 测试代码
int main() {
    vector<int> nums = {3, 2, 5, 1, 4};
    quickSort(nums);
    for (int num : nums) {
        cout << num << " ";
    }
    cout << endl; // 输出：1 2 3 4 5
    return 0;
}
```
#### 归并排序 O(nlogn)
```csharp
```
#### 堆排序 O(nlogn)
```csharp
```
#### 计数排序 O(n+k)
```csharp
```
#### 桶排序 O(n+k)
```csharp
```
#### 基数排序 O(dn)
```csharp
```

## 游戏相关算法
### 寻路
### 光栅化
### 人工智能