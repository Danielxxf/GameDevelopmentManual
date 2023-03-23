# 游戏编码（Game Coding）
游戏编码涉及到了数据结构和算法，和一些应用于游戏特定场景的算法。

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
    bool sorted;
    for(int i = 0; i < nums.Length - 1; i++){
        sorted = true;
        for(int j = 0; j < num.Length - 1; j++){
            if(nums[j] > nums[j + 1]){
                int t = nums[j];
                nums[j] = nums[j + 1];
                nums[j + 1] = t;
                sorted = false;
            }
        }
        if(sorted) return;
    }
}
```
#### 插入排序 O(n^2)
```csharp
```
#### 选择排序 O(n^2)
```csharp
```
#### 快速排序 O(nlogn)
```csharp
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

## 游戏算法
### 寻路
### 光栅化
### 人工智能