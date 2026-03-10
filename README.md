#  Java-Interview------Top coding
[TOC]

## 前言

#### 数据结构构造

##### 链表

###### **python**

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

def list_to_linked_list(arr):
    dum = head = ListNode(0)
    for a in arr:
        node = ListNode(a)
        head.next = node
        head = head.next
    return dum.next

def linked_list_to_list(head):
    arr = []
    while head:
        arr.append(head.val)
        head = head.next
    return arr

```

###### **java**

```java
public class ListNode {
    public int val;
    public ListNode next;
    
    public ListNode(int x) {
        val = x;
    }
    
    public static ListNode arrToLinkedList(int[] arr) {
        ListNode dum = new ListNode(0);
        ListNode head = dum;
        for (int val : arr) {
            head.next = new ListNode(val);
            head = head.next;
        }
        return dum.next;
    }

    public static ListNode getListNode(ListNode head, int val) {
        while (head != null && head.val != val) {
            head = head.next;
        }
        return head;
    }
}
```

##### 树

###### **python**

```python
import collections

class TreeNode: 
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def list_to_tree(arr):
    if not arr:
        return
    i = 1
    root = TreeNode(int(arr[0]))
    queue = collections.deque()
    queue.append(root)
    while queue:
        node = queue.popleft()
        if arr[i] != None:
            node.left = TreeNode(int(arr[i]))
            queue.append(node.left)
        i += 1
        if arr[i] != None:
            node.right = TreeNode(int(arr[i]))
            queue.append(node.right)
        i += 1
    return root

def tree_to_list(root):
    if not root: return []
    queue = collections.deque()
    queue.append(root)
    res = []
    while queue:
        node = queue.popleft()
        if node:
            res.append(node.val)
            queue.append(node.left)
            queue.append(node.right)
        else: res.append(None)
    return res
```

###### **java**

```java
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.List;
import java.util.Queue;

public class Main {
    public static void main(String[] args) {
        Treenode root = Treenode.arrToTree(new Integer[] { 4, 2, 7, 1, 3, 6, 9, null, null, null, null, null, null, null, null });
        Treenode res = mirrorTree(root);
        System.out.println(Treenode.treeToList(res));
    }

    public static Treenode mirrorTree(Treenode root) {
        if(root == null) return null;
        Treenode tmp = root.left;
        root.left = mirrorTree(root.right);
        root.right = mirrorTree(tmp);
        return root;
    }
}

class Treenode{
    public int val;
    public Treenode left;
    public Treenode right;
    public Treenode(int x){
        val = x;
    }

    public static Treenode arrToTree(Integer[] arr) {
        Treenode root = new Treenode(arr[0]);
        Queue<Treenode> queue = new LinkedList<Treenode>() {{ add(root); }};
        int i = 1;
        while(!queue.isEmpty()) {
            Treenode node = queue.poll();
            if(arr[i] != null) {
                node.left = new Treenode(arr[i]);
                queue.add(node.left);
            }
            i++;
            if(arr[i] != null) {
                node.right = new Treenode(arr[i]);
                queue.add(node.right);
            }
            i++;
        }
        return root;
    }

    public static List<Integer> treeToList(Treenode root) {
        List<Integer> list = new ArrayList<>();
        if(root == null) return list;
        Queue<Treenode> queue = new LinkedList<>();
        queue.add(root);
        while(!queue.isEmpty()) {
            Treenode node = queue.poll();
            if(node != null) {
                list.add(node.val);
                queue.add(node.left);
                queue.add(node.right);
            }
            else {
                list.add(null);
            }
        }
        return list;
    }
}
```



#### 如何准备

![image-20210617094311256](https://i.loli.net/2021/06/17/bxGQMJDtied7FR3.png)

> **当你没有思路时：**
>
> 给自己几个简单的测试用例，试验一下
>
> 不要忽略暴力解法，暴力解法通常是思考的起点

![image-20210617095424793](https://i.loli.net/2021/06/17/DQMGovnKWUEZakf.png)

![image-20210617095556710](https://i.loli.net/2021/06/17/iJ7L3vnDKdaOhmc.png)

#### 复杂度分析

![image-20210617111749816](https://i.loli.net/2021/06/17/bvgldcKjZGnCS71.png)



## 排序与查找算法：

#### [排序算法](https://www.cnblogs.com/guoyaohua/p/8600214.html#:~:text=%E5%8D%81%E5%A4%A7%E7%BB%8F%E5%85%B8%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95%E6%9C%80%E5%BC%BA%E6%80%BB%E7%BB%93%EF%BC%88%E5%90%ABJAVA%E4%BB%A3%E7%A0%81%E5%AE%9E%E7%8E%B0%EF%BC%89%201%20%E3%80%81%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95%E8%AF%B4%E6%98%8E%202%20%E3%80%81%E5%86%92%E6%B3%A1%E6%8E%92%E5%BA%8F%EF%BC%88Bubble%20Sort%EF%BC%89%203%20%E3%80%81%E9%80%89%E6%8B%A9%E6%8E%92%E5%BA%8F%EF%BC%88Selection,%E3%80%81%E8%AE%A1%E6%95%B0%E6%8E%92%E5%BA%8F%EF%BC%88Counting%20Sort%EF%BC%89%2010%20%E3%80%81%E6%A1%B6%E6%8E%92%E5%BA%8F%EF%BC%88Bucket%20Sort%EF%BC%89%2011%20%E3%80%81%E5%9F%BA%E6%95%B0%E6%8E%92%E5%BA%8F%EF%BC%88Radix%20Sort%EF%BC%89)

![image-20210617091803408](https://i.loli.net/2021/06/17/GkFbTlIcDo176Jv.png)


**放水排序：选择排序和冒泡排序**

都是O(n^2)的稳定排序，**选择排序是每次遍历找出最小的数放在最左边，冒泡排序是找到最大的数放到最右边**

```java
public static int[] selectSort(int[] arr) {
    // 外侧循环 起始点分别是0~l
    for (int i =0; i<arr.length-1; i++){
        // 先假设最小值是start_i
        int mini = i;
        for (int j=i+1;j<arr.length;j++) {
            if (arr[j]<arr[mini]) mini = j;
        }
        swap(arr,mini,i);
    }
    return arr;
}
```
冒泡排序其实差不多，只是内侧循环结束点为 len-i
```java
public static int[] bubbleSort(int[] arr) {
        if (arr ==null || arr.length<2) return arr;
        for (int i = 0; i < arr.length; i++) {
            for (int j = 0; j < arr.length - i - 1; j++) {
                if (arr[j+1]<arr[j]) swap(arr,j,j+1);
            }
        }
        return arr;
    }
```

**插入排序**

```java
    public static int[] insertSort(int[] arr) {
        if (arr ==null || arr.length<2) return arr;
        for (int i = 1; i < arr.length; i++) {
            int tem = arr[i];
            int k = i - 1;
            // 如果当前值（tem）小于 前面的元素 那么退退退
            while (k >= 0 && arr[k] > tem) {
                k--;
            }
//           腾出位置插进去,要插的位置是 k + 1; 
            for (int j = i; j > k + 1; j--) {
                arr[j] = arr[j - 1];
            }
//            插入
            arr[k+1] = tem;
        }
        return arr;
    }
```

**快速排序:**
- 大小比较时候是小于等于，这样一开始 i 才能移动
- 必须加内部 `i<j `的判断，不然j停下来之后，如果元素一直小于基准点，那么i会走的超过j
- 必须先运行j的查找动作，因为我们最终要跟左边元素交换，希望停下来元素要比基准点小，如果i在前面，那么他会使得停到比基准点大的元素那里了
- partition开始要记录下左边界，交换完后放到中间

```python 
def quickSort(nums,l,r):
        if l > r:return
        i = l ; j = r
        while i<j:
            while i<j and nums[j] >= nums[l]: j -= 1
            while i<j and nums[i] <= nums[l]: i += 1
            nums[i],nums[j] = nums[j],nums[i]
        nums[i],nums[l] = nums[l],nums[i]
        quickSort(nums, l, i - 1)
        quickSort(nums, i + 1, r)

if __name__ == '__main__':
    arr = [1,5,2,5,3,8,1,99,-6,-2]
    quickSort(arr,0,len(arr)-1)
    print(arr)
```

```java
public class Sort {
    public static void main(String[] args) {
        int[] oldArr = new int[]{2, 3, 4, 5, 1, 1, 0, -2};
        quickSort(oldArr,0,oldArr.length-1);
        System.out.println(Arrays.toString(oldArr));
    }

    private static void quickSort(int[] arr,int l,int r) {
        if (l > r) return;
        int i = l, j = r;
        while (i < j) {
            while (i < j && arr[j] >= arr[l]) j--;
            while (i < j && arr[i] <= arr[l]) i++;
            swap(arr, i, j);
        }
        swap(arr,i,l);
        quickSort(arr, l, i - 1);
        quickSort(arr, i + 1, r);
    }

    private static void swap(int[] arr, int i, int j) {
        int tem = arr[i];
        arr[i] = arr[j];
        arr[j] = tem;
    }
}
```

**归并排序**
归并排序其实就是合并两个有序数组，调用递归不停的拆分原数组，只剩一个的时候进行merge，再merge。
```python
def mergeSort(arr):
    if len(arr) == 1: return arr
    mid = len(arr)//2
    left = arr[:mid]
    right = arr[mid:]
    return merge(mergeSort(left),mergeSort(right))

def merge(left,right):
    result = []
    while len(left) > 0 and len(right) > 0:
        if left[0] <= right[0]:result.append(left.pop(0))
        else: result.append(right.pop(0))
    result += left
    result += right
    return result
if __name__ == '__main__':
    arr = [1,5,2,5,3,8,1,99,-6,-2]
    arr = mergeSort(arr)
    print(arr)
```

```java
public class Sort {
   public static void main(String[] args) {
      int[] oldArr = new int[]{2, 3, 4, 5, 1, 1, 0, -2};
//        quickSort(oldArr,0,oldArr.length-1);
      mergeSort(oldArr);
      System.out.println(Arrays.toString(oldArr));
   }

   public static void mergeSort(int[] array) {
      if (array == null || array.length <= 1) {
         return;
      }
      sort(array, 0, array.length - 1);
   }

   private static void sort(int[] array, int left, int right) {
      if (left == right) {
         return;
      }
      int mid = left + ((right - left) >> 1);
      // 对左侧子序列进行递归排序
      sort(array, left, mid);
      // 对右侧子序列进行递归排序
      sort(array, mid + 1, right);
      // 合并
      merge(array, left, mid, right);
   }

   private static void merge(int[] array, int left, int mid, int right) {
      int[] temp = new int[right - left + 1];
      int i = 0;
      int p1 = left;
      int p2 = mid + 1;
      // 比较左右两部分的元素，哪个小，把那个元素填入temp中
      while (p1 <= mid && p2 <= right) {
         temp[i++] = array[p1] < array[p2] ? array[p1++] : array[p2++];
      }
      // 上面的循环退出后，把剩余的元素依次填入到temp中
      // 以下两个while只有一个会执行
      while (p1 <= mid) {
         temp[i++] = array[p1++];
      }
      while (p2 <= right) {
         temp[i++] = array[p2++];
      }
      // 把最终的排序的结果复制给原数组
      for (i = 0; i < temp.length; i++) {
         array[left + i] = temp[i];
      }
   }
}
```
#### 快排兄弟——[最小的k个数](https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/)
定义一个三方函数，入参为nums,l,r，调用快排核心代码进行判断即可
```python
class Solution:
    def getLeastNumbers(self, arr: List[int], k: int) -> List[int]:
        if k == 0: return []
        def help(nums,l,r):
            i = l ; j = r
            while i<j:
                while i<j awhile i<j and nums[i] <= nums[l]: i += 1
                nums[i],nums[j] = nums[j],nums[i]
            nums[i],nums[l] = nums[l],nums[i]
            if i == k-1: return nums[:k]
            elif i < k-1:return  help(nums,i+1,r)
            else: return help(nums,l,i-1)
        return help(arr,0,len(arr)-1)
```
```java
class Solution {
    public int[] getLeastNumbers(int[] arr, int k) {
        help(arr, 0, arr.length - 1, k);
        return Arrays.copyOf(arr, k);
    }

    public void help(int[] arr, int l, int r, int k) {
        if(l >= r) return;
        int i = l, j = r;
        while (i < j) {
            while (i<j && arr[j] >= arr[l]) j--;
            while (i<j && arr[i] <= arr[l]) i++;
            swap(arr, i, j);
        }
        swap(arr,i,l);
        if(i < k)  help(arr, i + 1, r, k);
        else help(arr, l, i - 1, k);
    }

    public void swap(int[] arr, int i, int j) {
        int tem = arr[i];
        arr[i] = arr[j];
        arr[j] = tem;
    }
}
```
为对比学习列出[寻找第K大](https://leetcode-cn.com/problems/kth-largest-element-in-an-array/submissions/)的代码：

```python
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        if k == 0: return []
        def help(nums,l,r):
            i = l ; j = r
            while i<j:
                while i<j and nums[j] <= nums[l]: j -= 1
                while i<j and nums[i] >= nums[l]: i += 1
                nums[i],nums[j] = nums[j],nums[i]
            nums[i],nums[l] = nums[l],nums[i]
            if i == k-1: return nums[k-1]
            elif i < k-1:return  help(nums,i+1,r)
            else: return help(nums,l,i-1)
        return help(nums,0,len(nums)-1)
```

```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        help(nums, 0, nums.length-1, k);
        return nums[k-1];
    }

    public void help(int[] arr, int l, int r, int k) {
        if(l >= r) return;
        int i = l, j = r;
        while (i < j) {
            while (i<j && arr[j] <= arr[l]) j--;
            while (i<j && arr[i] >= arr[l]) i++;
            swap(arr, i, j);
        }
        swap(arr,i,l);
        if(i < k)  help(arr, i + 1, r, k);
        else help(arr, l, i - 1, k);
    }

    public void swap(int[] arr, int i, int j) {
        int tem = arr[i];
        arr[i] = arr[j];
        arr[j] = tem;
    }
}
```
#### 你看不出来的快排--[ 把数组排成最小的数](https://leetcode-cn.com/problems/ba-shu-zu-pai-cheng-zui-xiao-de-shu-lcof/)
快排，重新定义数的大小即可
如果 a+b > b+a 则 a > b 因为要排成ba
![img.png](img.png)
```python
class Solution:
    def minNumber(self, nums: List[int]) -> str:
        def quick_sort(l , r):
            if l >= r: return
            i, j = l, r
            while i < j:
                while strs[j] + strs[l] >= strs[l] + strs[j] and i < j: j -= 1
                while strs[i] + strs[l] <= strs[l] + strs[i] and i < j: i += 1
                strs[i], strs[j] = strs[j], strs[i]
            strs[i], strs[l] = strs[l], strs[i]
            quick_sort(l, i - 1)
            quick_sort(i + 1, r)
   
        strs = [str(num) for num in nums]
        quick_sort(0, len(strs) - 1)
        return ''.join(strs)
```

#### 二分查找算法：

关注 **大于等于号** **是否加一**

本文对应的力扣题目：

[704.二分查找](https://leetcode-cn.com/problems/binary-search)

[34.在排序数组中查找元素的第一个和最后一个位置](https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

1.6.1 二分查找框架

```java
int binarySearch(int[] nums, int target) {
    int left = 0, right = ...;
    while(...) {
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) {
            ...
        } else if (nums[mid] < target) {
            left = ...
        } else if (nums[mid] > target) {
            right = ...
        }
    }
    return ...;
}
```

1.6.2 寻找一个数（基本的二分搜索）

这个场景是最简单的，可能也是大家最熟悉的，即搜索一个数，如果存在，则返回其索引，否则返回 -1。

```java
int binarySearch(int[] nums, int target) {
    int left = 0; 
    int right = nums.length - 1; // 注意

    while(left <= right) {
        int mid = left + (right - left) / 2;
        if(nums[mid] == target)
            return mid; 
        else if (nums[mid] < target)
            left = mid + 1; // 注意
        else if (nums[mid] > target)
            right = mid - 1; // 注意
    }
    return -1;
}
```

1.6.3 寻找左侧边界的二分搜索

以下是最常见的代码形式，其中的标记是需要注意的细节：

```java
int left_bound(int[] nums, int target) {
    if (nums.length == 0) return -1;
    int left = 0;
    int right = nums.length; // 注意
    
    while (left < right) { // 注意
        int mid = (left + right) / 2;
        if (nums[mid] == target) {
            right = mid;
        } else if (nums[mid] < target) {
            left = mid + 1;
        } else if (nums[mid] > target) {
            right = mid; // 注意
        }
    }
    return left;
}
```

1.6.4 寻找右侧边界的二分查找

比较常见的左闭右开的写法，只有两处和搜索左侧边界不同，已标注：

```java
int right_bound(int[] nums, int target) {
    if (nums.length == 0) return -1;
    int left = 0, right = nums.length;
    
    while (left < right) {
        int mid = (left + right) / 2;
        if (nums[mid] == target) {
            left = mid + 1; // 注意
        } else if (nums[mid] < target) {
            left = mid + 1;
        } else if (nums[mid] > target) {
            right = mid;
        }
    }
    return left - 1; // 注意
}
```

**我们还根据逻辑将「搜索区间」全都统一成了两端都闭，便于记忆，只要修改两处即可变化出三种写法**：

```java
int binary_search(int[] nums, int target) {
    int left = 0, right = nums.length - 1; 
    while(left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] < target) {
            left = mid + 1;
        } else if (nums[mid] > target) {
            right = mid - 1; 
        } else if(nums[mid] == target) {
            // 直接返回
            return mid;
        }
    }
    // 直接返回
    return -1;
}

int left_bound(int[] nums, int target) {
    int left = 0, right = nums.length - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] < target) {
            left = mid + 1;
        } else if (nums[mid] > target) {
            right = mid - 1;
        } else if (nums[mid] == target) {
            // 别返回，收紧右边界，锁定左侧边界
            right = mid - 1;
        }
    }
    // 最后要检查 left 越界的情况
    if (left >= nums.length || nums[left] != target)
        return -1;
    return left;
}


int right_bound(int[] nums, int target) {
    int left = 0, right = nums.length - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] < target) {
            left = mid + 1;
        } else if (nums[mid] > target) {
            right = mid - 1;
        } else if (nums[mid] == target) {
            // 别返回，收紧左边界，锁定右侧边界
            left = mid + 1;
        }
    }
    // 最后要检查 right 越界的情况
    if (right < 0 || nums[right] != target)
        return -1;
    return right;
}
```

#### [在排序数组中查找元素的第一个和最后一个位置](https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

```python
class Solution:
    def searchRange(self, nums: List[int], target: int) -> List[int]:
        l = 0; r = len(nums)-1
        while l <= r:
            mid = l + (r-l)//2
            if nums[mid] == target:
                lbindry = mid; rbindry = mid
                while lbindry >= 0 and nums[lbindry] == target: lbindry -= 1
                while rbindry < len(nums) and nums[rbindry] == target: rbindry += 1
                return [lbindry+1,rbindry-1]
            elif nums[mid] < target:  l = mid+1
            else: r = mid -1
        return [-1,-1]
```

**解法二 java 左右边界分别考虑**

```java
lass Solution {
    public int[] searchRange(int[] nums, int target) {
        return new int[]{findl(nums,target),findr(nums,target)};
    }

    int findl(int[] nums, int target){
        int l = 0, r = nums.length-1;
        while(l <= r){
            int mid = (l+r)>>1;
            if(nums[mid] == target) r--;
            else if(nums[mid] > target) r = mid-1;
            else l = mid+1;
        }
        // if(l >= nums.length ) return -1;
        if(l >= nums.length || nums[l] != target) return -1;
        return l;
    }

    int findr(int[] nums, int target){
        int l = 0, r = nums.length-1;
        while(l <= r){
            int mid = (l+r)>>1;
            if(nums[mid] == target) l++;
            else if(nums[mid] > target) r = mid-1;
            else l = mid+1;
        }
        if(r < 0 || nums[r] != target) return -1;
        // if(r < 0 ) return -1;
        return r;
    }
}
```

#### 旋转数组

33 题，81题，查找特定值：
使用左闭右闭区间
比较中间值与左侧值，如果等于就收缩左边区间
如果大于，{l:mid} 单调递增，看看target是否在这个区间，在则 r = mid-1
否则单调区间在右侧
```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        l = 0; r = len(nums)-1
        while l<=r:
            mid = l+(r-l)//2 
            if nums[mid] == target: return mid
            if nums[l] == nums[mid]:
                l += 1
                continue
            elif nums[l] < nums[mid]:
                if target >= nums[l] and target <= nums[mid]: r = mid-1
                else: l = mid +1
            else:
                if nums[mid] <= target and nums[r] >= target: l = mid+1
                else: r = mid-1
        return -1
```
java solution
```java
class Solution {
    public int search(int[] nums, int target) {
        int l = 0, r = nums.length-1;
//        这里有等于号
        while (l <= r) {
//            这里不建议用位运算
            int mid = l + (r-l)/2;
            if(nums[mid] == target) return mid;
            if (nums[mid] == nums[l]) {
                l++;
            } else if (nums[mid] > nums[l]) {
//                这里也有等于号
                if (target >= nums[l] && target <= nums[mid]) r = mid - 1;
                else l = mid + 1;
            } else {
                if (target >= nums[mid] && target <= nums[r]) l = mid + 1;
                else r = mid - 1;
            }
        }
        return -1;
    }
}
```

153 题，154题 查找最小值：
使用左闭右闭区间
如果中间值大于右侧值，说明肯定不在左区间
小于 不确定在哪个区间，所以收缩r到mid
如果等于 只能逐渐收缩

```python
    def findMin(self, nums: List[int]) -> int:
        left, right = 0, len(nums) - 1
        while left <= right:
            mid = (left + right) // 2
            if nums[mid] > nums[right]: left = mid + 1
            elif nums[mid] < nums[right]: right = mid
            else: right = right - 1 # key
        return nums[left]
```

```java
class Solution {
    public int minArray(int[] numbers) {
        int l = 0, r = numbers.length-1;
        while(l <= r){
            int mid = (l+r)>>1;
            if(numbers[mid] > numbers[r]) l = mid+1;
            else if(numbers[mid]< numbers[r]) r = mid;
            else r--;
        }
        return numbers[l];
    }
}
```
另一种做法
```python
class Solution:
#  本题寻找最小值，最小值只会出现在非递增区间，因此和Q33题相反，需要寻找非递增的情况
#  如果没有发生旋转: 1 2 3 4 5 6, low对应的值一定小于high
    def minArray(self, nums: List[int]) -> int:
        l = 0; r = len(nums)-1
        # 剩下最后一个就是结果
        while l< r:
    # 这里也去掉了相等的条件
            if nums[r] > nums[l]: return nums[l]
            mid = l +(r-l)//2
            if nums[l] == nums [mid]:
                l += 1 #相等的时候，low ++，跳过干扰项
                continue
            if nums[mid] > nums[l]: l = mid+1 #递增区间，最小值不会出现在这
            else: r = mid #无法排除mid
        return nums[l]
```

#### [寻找峰值](https://leetcode-cn.com/problems/find-peak-element/)
- 使用左闭右开区间
- 比较中间值与他的左侧即可
- 如果大于说明肯定不在左区间
- 小于或者等于不好说，但是可以把r收缩到mid
```python
class Solution:
    def findPeakElement(self, nums: List[int]) -> int:
        l = 0; r = len(nums)
        while l < r:
            mid = l+(r-l)//2
            if nums[mid] > nums[mid-1]: l = mid+1
            else: r= mid
        return l-1 if l != 0 else 0
```
java
```java
class Solution {
    public int findPeakElement(int[] nums) {
//        这道题用的是左开右开区间
        int l = 0, r = nums.length;
        while (l < r) {
            int mid = (r+l)/2;
//            如果是java这里需要判断越界异常，因为python有[-1]
            if(mid > 0 && nums[mid] > nums[mid-1]) l = mid+1;
            else r = mid;
        }
        if(l > 0 ) return l - 1;
        return 0;
    }
}
```
#### [0～n-1中缺失的数字](https://leetcode-cn.com/problems/que-shi-de-shu-zi-lcof/)

![image-20220319115401434](http://pic.wyydd.top/image-20220319115401434.png)

```java
class Solution {
    public int missingNumber(int[] nums) {
        int i = 0, j = nums.length - 1;
        while(i <= j) {
            int m = (i + j) / 2;
            if(nums[m] == m) i = m + 1;
            else j = m - 1;
        }
        return i;
    }
}

public class sfo_53ii_the_missing_number_from_0_to_n1_s1 {
    public static void main(String[] args) {
        // ======= Test Case =======
        int[] nums = { 0, 1, 3 };
        // ====== Driver Code ======
        Solution slt = new Solution();
        int res = slt.missingNumber(nums);
        System.out.println(res);
    }
}
```

#### [ x 的平方根 ](https://leetcode-cn.com/problems/sqrtx/)

**解法一：二分法**

```python
class Solution:
    def mySqrt(self, x: int) -> int:
        l = 0
        r = x
        while l <= r:
            mid = (l+r)//2
            temp = mid**2
            if  temp < x:
                l = mid + 1
            elif temp > x:
                r = mid - 1
            elif temp == x:
                return mid
        # r一定会停在mid**2 <= x的最大那个mid的位置，因为mid**2=x的mid如果存在的话在上面
        # 就已经返回了，所以这里只需要返回r就好了
        return r 
```

**这道题一定要注意 保留到小数点后几位的变形体**

**解法二：牛顿迭代法**

![image-20220322103304432](http://pic.wyydd.top/image-20220322103304432.png)

```python
class Solution:
    def mySqrt(self, x: int) -> int:
        if x == 0: return 0
        x0 = float(x)
        while 1:
            x1 = (x0 + x/x0)*0.5
            if abs(x1-x0)<1e-3:
                return '%.3f'%x1
            x0 = x1
```

## 数组相关的算法：

#### [两数之和](https://www.nowcoder.com/practice/20ef0972485e41019e39543e8e895b7f?tpId=117&&tqId=37756&rp=1&ru=/ta/job-code-high&qru=/ta/job-code-high/question-ranking)
遍历的时候用个hasmap存储一下，然后判断target-nums[i]在不在就好了
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer,Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            if (map.containsKey(target - nums[i])) {
                return new int[]{i, map.get(target - nums[i])};
            }
            map.put(nums[i], i);
        }
        return new int[]{-1, -1};
    }
}
```
python解法
```python
class Solution:
    #     解法1 暴力解法
    def twoSum(self , numbers , target ):        
        for i in range(len(numbers)):
            for j in range(i+1,len(numbers)):
                if(numbers[i]+numbers[j] == target):return[i+1,j+1]
                
#     解法2 ：空间换时间
    def twoSum(self , numbers , target ):
        Hmap = dict()
        for i,num in enumerate(numbers):
            Hmap[num] = i
        for i in range(len(numbers)):
            index = target - numbers[i]
            if index in Hmap.keys() and Hmap[index] != i:
                return[i+1,Hmap[index]+1]
        return None
```

#### [三数之和](https://leetcode-cn.com/problems/3sum/)

这题最关键的是去重 排序-->首尾双指针--->去重

```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        res = []
        nums.sort()
        for k in range(len(nums)-2):
            if nums[k] > 0: break
            if k > 0 and nums[k] == nums[k-1]: continue
            i = k+1; j = len(nums)-1
            while i < j:
                if nums[i]+nums[j]+nums[k] == 0:
                    res.append([nums[k],nums[i],nums[j]])
                    while i+1 < len(nums)-1 and nums[i+1] == nums[i]: i+=1
                    while j-1 > 0 and nums[j-1] == nums[j]: j-=1
                    i += 1; j -= 1
                if nums[i]+nums[j]+nums[k] > 0: j -= 1
                if nums[i]+nums[j]+nums[k] < 0: i += 1
        return res
```
java 解法
```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
//        Java api
        List<List<Integer>> res = new ArrayList<>();
        Arrays.sort(nums);
        for (int k = 0; k < nums.length - 2; k++) {
            if(nums[k] > 0) break;
//            对k去重
            if (k > 0 && nums[k] == nums[k - 1]) continue;
            int i = k + 1, j = nums.length - 1;
            while (i < j) {
                if (nums[k] + nums[i] + nums[j] == 0) {
//                    java api
                    res.add(new ArrayList<Integer>(Arrays.asList(nums[i],nums[j],nums[k])));
//                    对 i j去重
                    while (i+1 < nums.length-1 && nums[i+1] == nums[i]) i++;
                    while (j-1 > 0 && nums[j-1] == nums[j]) j--;
//                    i 和 j还在相等数字的边界处
                    i++; j--;
                }
                if (nums[k] + nums[i] + nums[j] > 0) j--;
                if (nums[k] + nums[i] + nums[j] < 0) i++;
            }
        }
        return res;
    }
}
```

#### [剑指 Offer 21. 调整数组顺序使奇数位于偶数前面](https://leetcode-cn.com/problems/diao-zheng-shu-zu-shun-xu-shi-qi-shu-wei-yu-ou-shu-qian-mian-lcof/)

```java
/**
     * 可以满足奇数位于偶数前面的算法，但是奇数和奇数、偶数和偶数的相对位置不能保证。
     * 时间复杂度O(N)，空间O(1)
     * @param arr
     */
    private static void reOrderArray(int[] arr){
        if(arr==null||arr.length<2)
            return ;
        int left = 0;
        int right = arr.length-1;
        while(left<right){
            while((arr[left]&1)==1){
                left++;
            } 
            while((arr[right]&1)==0){
                right--;
            }
            // 如果不加此处的if判断语句，会导致right已经在left前面了，但是依然进行了交换。
            // 即将已经在前面的奇数和后面的偶数进行了置换！！！
            if(left<right){
                int temp = arr[left];
                arr[left] = arr[right];
                arr[right] = temp;
            }
        }
    }
```

#### [剑指 Offer 39. 数组中出现次数超过一半的数字](https://leetcode-cn.com/problems/shu-zu-zhong-chu-xian-ci-shu-chao-guo-yi-ban-de-shu-zi-lcof/)
- 哈希表统计法： 遍历数组 nums ，用 HashMap 统计各数字的数量，即可找出 众数 。此方法时间和空间复杂度均为 O(N)O(N) 。
- 数组排序法： 将数组 nums 排序，数组中点的元素 一定为众数。
- 摩尔投票法： 核心理念为 票数正负抵消 。此方法时间和空间复杂度分别为 O(N)O(N) 和 O(1)O(1) ，为本题的最佳解法。
* 众数投一票正的，非众数投一票负的，则遍历完总票数一定为正，当
且当总票数为零的时候，剩余数字的众数一定不变
  
```java
class Solution {
    public int majorityElement(int[] nums) {
        int x = 0, votes = 0;
        for(int num : nums){
            if(votes == 0) x = num;
            votes += num == x ? 1 : -1;
        }
        return x;
    }
}
```
```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        score = 0
        for i in range(len(nums)):
            if score == 0: res = nums[i]
            score = score+1 if nums[i] == res else score-1
        return res
```

#### [删除有序数组中的重复项](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/)
fast从左到右一次遍历，slow开始处于0，如果fast和slow不相等就
**先slow++，然后fast赋值**

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        int slow = 0;
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] != nums[slow]) {
                slow++;
                nums[slow] = nums[i];
            }
        }
        return slow+1;
    }
}
```
python解法
```python
  class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        slow = 0
        for i in range(1,len(nums)):
            if nums[i] != nums[slow]:
                slow += 1
                nums[slow] = nums[i]
        nums = nums[:slow]
        return slow+1
```

#### [数组中重复的数字](https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/)

在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内,所以可以用一个萝卜一个坑的思路，让索引和数一一对应起来，若被占了，说明重复

```python
class Solution:
    def findRepeatNumber(self, nums: List[int]) -> int:
        for i in range(len(nums)):
            #这一步的判断很关键，防止本来人家位置就坐的对着
            if nums[i] == i:continue
            elif nums[nums[i]] == nums[i]:
                return nums[i]
            nums[nums[i]],nums[i] = nums[i],nums[nums[i]]
```
java解法
```java
class Solution {
    public int findRepeatNumber(int[] nums) {
        for (int i = 0; i < nums.length; i++) {
            if(nums[i] == i) continue;
            else if(nums[i] == nums[nums[i]]) return nums[i];
            swap(nums,nums[i],i);
        }
        return 0;
    }

    public void swap(int[] nums, int i, int j) {
        int tem = nums[i];
        nums[i] = nums[j];
        nums[j]= tem;
    }
}
```
**再来一道原地交换的题目**

#### [缺失的第一个正数](https://leetcode-cn.com/problems/first-missing-positive/)
- 首先，不要害怕，这道题虽然写的困难，但是不难。
- 我们要找到缺失的第一个正数，肯定是从1开始找，如果里面数字都特别大，那返回1就行了
- 所以，关键其实是找到里面比较小的那些数，只有他们才有可能是答案
- 因此先一遍遍历，找到nums[i]该被放入的位置(其索引应该是i-1)
- 遍历结束后，如果有不该返回的正数，那么他一定在自己该放入的位置，继续遍历，只要位置不对，那按顺讯返回第一个不对的位置就好了
- 最后如果比较碰巧，用完了数组都没找到，那肯定是数组长度加一是返回值了，也就是刚好有序的情况
```Python 
class Solution:
    def firstMissingPositive(self, nums: List[int]) -> int:
        for i in range(len(nums)):
            while 0<nums[i]<=len(nums) and nums[nums[i]-1] != nums[i]:
                # 原地交换有依赖关系的时候要注意顺序
                # nums[i],nums[nums[i]-1] = nums[nums[i]-1],nums[i]
                nums[nums[i]-1],nums[i] = nums[i],nums[nums[i]-1]
        for i in range(len(nums)):
            if nums[i] != i+1: return i+1
        # 如果刚好全部有序 则返回数组长度加一
        return i+2
```
java解法
```java
class Solution {
    public int firstMissingPositive(int[] nums) {
        for (int i = 0; i < nums.length; i++) {
            while (0 < nums[i] && nums[i] <= nums.length && nums[i] != nums[nums[i] - 1]) {
                int tem = nums[nums[i] - 1];
                nums[nums[i] - 1] = nums[i];
                nums[i] = tem;
            }
        }
        for (int i = 0; i < nums.length; i++) {
            if(nums[i] != i+1) return i+1;
        }
        return nums.length+1;
    }
}
```
#### [下一个排列](https://leetcode-cn.com/problems/next-permutation/)--排序函数是否原地操作

**[优秀题解](https://leetcode-cn.com/problems/next-permutation/solution/xia-yi-ge-pai-lie-suan-fa-xiang-jie-si-lu-tui-dao-/)**

题干的意思是：找出这个数组排序出的所有数中，刚好比当前数大的那个数

标准的“下一个排列”算法可以描述为：

1. 从后向前查找第一个相邻升序的元素对 (i,j)，满足 A[i] < A[j]。此时 [j,end) 必然是降序

2. 在 [j,end) 从后向前查找第一个满足 A[i] < A[k] 的 k。A[i]、A[k] 分别就是上文所说的「小数」、「大数」
3. 将 A[i] 与 A[k] 交换
4. 可以断定这时 [j,end) 必然是降序，逆置 [j,end)，使其升序
5. 如果在步骤 1 找不到符合的相邻元素对，说明当前 [begin,end) 为一个降序顺序，则直接跳到步骤 4

![image.png](https://pic.leetcode-cn.com/e56a66ed318d1761cd8c8f9d1521f82a30c71ecc84f551912b90d8fe254c8f3d-image.png)

**总结 list.sort()是原地操作，sorted(list)不是，但是list[切片].sort()不是原地操作**

```python
class Solution:
    def nextPermutation(self, nums: List[int]) -> None:
        length = len(nums)
        if length <= 1: return
        i = length-2; j = length-1; k = length-1
        while i >= 0 and nums[i] >= nums[j]:
            i -= 1
            j -= 1
        if i >= 0:
            while nums[i] >= nums[k]: k -= 1
            nums[i],nums[k] = nums[k],nums[i]
         # 逆序nums[j:] 但一定要注意这里不是原地操作，但是num.sort()其实是原地操作
        tem = sorted(nums[j:])
        nums[j:] = tem
        
        # 或者就老老实实的写逆序函数
        # left, right = j, length - 1
        # while left < right:
        #     nums[left], nums[right] = nums[right], nums[left]
        #     left += 1
        #     right -= 1
```
java解法
```java
class Solution {
    public void nextPermutation(int[] nums) {
        int len = nums.length;
        if(len <= 1) return;
        int i = len - 2, j = len - 1, k = len - 1;
//        排除降序元素
        while (i >= 0 && nums[i] >= nums[j]) {
            i--; j--;
        }
        if (i >= 0) {
//            找到第一个大于num[i] 的k
            while (nums[i] >= nums[k]) k--;
//            交换
            int tem = nums[i]; nums[i] = nums[k];
            nums[k] = tem;
        }
        reverse(nums,j,len-1);
    }
    public void reverse(int[] nums, int left, int right) {
        for(int i = left; i < left + (right-left+1)/2; i++) {
            int temp = nums[i];
            nums[i] = nums[right-(i-left)];
            nums[right-(i-left)] = temp;
        }
    }
}
```
#### [接雨水](https://leetcode-cn.com/problems/trapping-rain-water/submissions/)

**核心**：每一个位置能盛最多水等于`min(lmax,rmax)-arr[i]`

```python
class Solution:
    def maxWater(self , arr ):
        res,size = 0, len(arr)
        l,r = 0,size-1
        lmax,rmax = arr[l],arr[r]
        while(l<r):
            lmax = max(lmax,arr[l])
            rmax = max(rmax,arr[r])
            if lmax<=rmax:
                res += lmax - arr[l]
                l += 1
            else:
                res += rmax -arr[r]
                r -= 1
        return res
```

```java
class Solution {
    public int trap(int[] height) {
        int l = 0, r = height.length-1, res = 0;
        int lmax = height[l], rmax = height[r];
        while (l<r){
            lmax = Math.max(lmax,height[l]);
            rmax = Math.max(rmax,height[r]);
            res += lmax<rmax?
                lmax-height[l++]:
                rmax-height[r--];
        }
        return res;
    }
}
```

#### [盛最多水的容器](https://leetcode-cn.com/problems/container-with-most-water/)

暴力解法：遍历所有，结果为（i-j)*min(heigth[i],height[j]),超时，影响因素有两个 距离 和最小值

初始化为数组两侧距离乘以最小值，不断内卷，距离在减小，所以只有最小值更新时结果才有可能更新，所以双指针解法，矮柱子索引内卷直到相遇

```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        i, j, res = 0, len(height) - 1, 0
        while i < j:
            if height[i] < height[j]:
                res = max(res, height[i] * (j - i))
                i += 1
            else:
                res = max(res, height[j] * (j - i))
                j -= 1
        return res
```

```java
class Solution {
    public int maxArea(int[] height) {
        int l = 0,r = height.length-1,res = 0;
        while(l<r){
            res = height[l] < height[r] ?
                Math.max(res, (r-l)*height[l++]):
                Math.max(res, (r-l)*height[r--]);
        }
        return res;
    }
}
```

#### [剑指 Offer 42. 连续子数组的最大和](https://leetcode-cn.com/problems/lian-xu-zi-shu-zu-de-zui-da-he-lcof/)

![Picture1.png](https://pic.leetcode-cn.com/8fec91e89a69d8695be2974de14b74905fcd60393921492bbe0338b0a628fd9a-Picture1.png)

```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        dp = [nums[0]]*len(nums)
        for i in range(1,len(nums)):
            dp[i] = max(dp[i-1]+nums[i],nums[i])
        return max(dp)
```

java代码

```java
class Solution {
    public int maxSubArray(int[] nums) {
        int res = nums[0];
        for(int i = 1; i<nums.length; i++){
            nums[i] += Math.max(nums[i-1],0);
            res = Math.max(res,nums[i]);
        }
        return res;
    }
}
```

**二维数组题目：**

#### [螺旋矩阵(顺时针打印矩阵)](https://leetcode.cn/problems/shun-shi-zhen-da-yin-ju-zhen-lcof/)

循环遍历并且用哨兵看着

| 打印方向 | 1. 根据边界打印        | 2. 边界向内收缩  | 3. 是否打印完毕 |
| -------- | ---------------------- | ---------------- | --------------- |
| 从左向右 | 左边界`l` ，右边界 `r` | 上边界 `t` 加 11 | 是否 `t > b`    |
| 从上向下 | 上边界 `t` ，下边界`b` | 右边界 `r` 减 11 | 是否 `l > r`    |
| 从右向左 | 右边界 `r` ，左边界`l` | 下边界 `b` 减 11 | 是否 `t > b`    |
| 从下向上 | 下边界 `b` ，上边界`t` | 左边界 `l` 加 11 | 是否 `l > r`    |

```python
class Solution:
    def spiralOrder(self , matrix ):
        if not matrix:return[]
        l,r,t,b,res = 0,len(matrix[0])-1,0,len(matrix)-1,[]
        while l<=r and t <= b:
            for i in range(l,r+1):res.append(matrix[t][i])
            t += 1
            # 这里需要判断是否结束
            if t > b: break
            for i in range(t,b+1):res.append(matrix[i][r])
            r -= 1
            if l>r: break
            for i in range(r,l-1,-1):res.append(matrix[b][i])
            b -= 1
            if t > b: break
            for i in range(b,t-1,-1):res.append(matrix[i][l])
            l += 1
            if l>r: break
        return res
```
java 代码

```java
class Solution {
    public int[] spiralOrder(int[][] matrix) {
        if(matrix.length == 0) return new int[0];
        int l = 0, r = matrix[0].length - 1, t = 0, b = matrix.length - 1, x = 0;
        int[] res = new int[(r + 1) * (b + 1)];
        while(true) {
            for(int i = l; i <= r; i++) res[x++] = matrix[t][i]; // left to right.
            if(++t > b) break;
            for(int i = t; i <= b; i++) res[x++] = matrix[i][r]; // top to bottom.
            if(l > --r) break;
            for(int i = r; i >= l; i--) res[x++] = matrix[b][i]; // right to left.
            if(t > --b) break;
            for(int i = b; i >= t; i--) res[x++] = matrix[i][l]; // bottom to top.
            if(++l > r) break;
        }
        return res;
    }
}
```

#### [旋转图像](https://leetcode-cn.com/problems/rotate-image/)

```
class Solution:
    def rotate(self, matrix: List[List[int]]) -> None:
        n = len(matrix)

# 先转置
        for i in range(n):
            for j in range(i+1,n):
                matrix[i][j],matrix[j][i] = matrix[j][i],matrix[i][j]
# 再镜像        
        for i in range(n):
            for j in range(n>>1):
                matrix[i][j],matrix[i][n-1-j] = matrix[i][n-1-j],matrix[i][j]
        
        return matrix
```
java解法
先把二维矩阵沿对角线反转，然后反转矩阵的每一行，结果就是顺时针反转整个矩阵。
```java
class Solution {
    public void rotate(int[][] matrix) {
        int n = matrix.length;
        // 先沿对角线反转二维矩阵
        for (int i = 0; i < n; i++) {
            for (int j = i; j < n; j++) {
                // swap(matrix[i][j], matrix[j][i]);
                int temp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = temp;
            }
        }
        // 然后反转二维矩阵的每一行
        for (int[] row : matrix) {
            reverse(row);
        }
    }

    // 反转一维数组
    void reverse(int[] arr) {
        int i = 0, j = arr.length - 1;
        while (j > i) {
            // swap(arr[i], arr[j]);
            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
            i++;
            j--;
        }
    }
}
```

#### [岛屿数量](https://leetcode-cn.com/problems/number-of-islands/)

解法一：淹水算法

```python
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        m = len(grid); n = len(grid[0]);res = 0
        visited = set()
        def foodfile(grid,i,j):
            if i < 0 or i >= m or j<0 or j>=n or grid[i][j] == '0' or (i,j) in visited:
                return
            visited.add((i,j))
            foodfile(grid,i-1,j) 
            foodfile(grid,i+1,j) 
            foodfile(grid,i,j-1) 
            foodfile(grid,i,j+1)  
        for i in range(m):
            for j in range(n):
                if grid[i][j] == '1' and not (i,j) in visited:
                    res += 1
                    foodfile(grid,i,j)
        return res
```

```java 
class Solution {
    public int numIslands(char[][] grid) {
        int count = 0;
        for(int i = 0; i < grid.length; i++) {
            for(int j = 0; j < grid[0].length; j++) {
                if(grid[i][j] == '1'){
                    dfs(grid, i, j);
                    count++;
                }
            }
        }
        return count;
    }
    private void dfs(char[][] grid, int i, int j){
        if(i < 0 || j < 0 || i >= grid.length || j >= grid[0].length || grid[i][j] == '0') return;
        grid[i][j] = '0';
        dfs(grid, i + 1, j);
        dfs(grid, i, j + 1);
        dfs(grid, i - 1, j);
        dfs(grid, i, j - 1);
    }
}
```

![image-20210614221953656](https://i.loli.net/2021/06/14/PjMr1lE5pWeyx2V.png)

解法二：并查集

![image-20210614222314950](images/image-20210614222314950.png)

![image-20210614222337661](images/image-20210614222337661.png)

#### [岛屿的最大面积](https://leetcode-cn.com/problems/max-area-of-island/)

```python
class Solution:
    def maxAreaOfIsland(self, grid: List[List[int]]) -> int:
        m = len(grid); n = len(grid[0])
        def recur(grid, i, j, tem):
            if grid[i][j] == 0: return
            grid[i][j] = 0
            tem[0] += 1
            if i+1 < m and grid[i + 1][j] == 1:recur(grid, i + 1, j, tem)      
            if j+1 < n and grid[i][j + 1] == 1:recur(grid, i, j + 1, tem)      
            if i-1 >= 0 and grid[i - 1][j] == 1: recur(grid, i - 1, j, tem)   
            if j-1 >= 0 and grid[i][j - 1] == 1:recur(grid, i, j - 1, tem)
            
        res = 0
        for i in range(len(grid)):
            for j in range(len(grid[0])):
                if grid[i][j] == 1:
                    tem = [0]
                    recur(grid, i, j, tem)
                    res = max(res, tem[0])
        return res
```

java

```java
class Solution {
    public int maxAreaOfIsland(int[][] grid) {
        // 记录岛屿的最大面积
        int res = 0;
        int m = grid.length, n = grid[0].length;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (grid[i][j] == 1) {
                    // 淹没岛屿，并更新最大岛屿面积
                    res = Math.max(res, dfs(grid, i, j));
                }
            }
        }
        return res;
    }

    // 淹没与 (i, j) 相邻的陆地，并返回淹没的陆地面积
    int dfs(int[][] grid, int i, int j) {
        int m = grid.length, n = grid[0].length;
        if (i < 0 || j < 0 || i >= m || j >= n) {
            // 超出索引边界
            return 0;
        }
        if (grid[i][j] == 0) {
            // 已经是海水了
            return 0;
        }
        // 将 (i, j) 变成海水
        grid[i][j] = 0;

        return dfs(grid, i + 1, j)
                + dfs(grid, i, j + 1)
                + dfs(grid, i - 1, j)
                + dfs(grid, i, j - 1) + 1;
    }
}
```

#### [太平洋大西洋水流问题](https://leetcode-cn.com/problems/pacific-atlantic-water-flow/)

```python
from  include import *
def pacificAtlantic(heights: List[List[int]]) -> List[List[int]]:
    m = len(heights)
    n = len(heights[0])
    isFillX = [[False] * n] * m
    isFillY = [[False] * n] * m

    def recur(heights, i, j, isFill):
        if isFill[i][j]: return
        isFill[i][j] = True
        if (i + 1 < m and heights[i + 1][j] >= heights[i][j]): recur(heights, i + 1, j, isFill)
        if (i - 1 >= 0 and heights[i - 1][j] >= heights[i][j]): recur(heights, i - 1, j, isFill)
        if (j + 1 < n and heights[i][j + 1] >= heights[i][j]): recur(heights, i, j + 1, isFill)
        if (j - 1 >= 0 and heights[i][j - 1] >= heights[i][j]): recur(heights, i, j - 1, isFill)

    for i in range(m):
        recur(heights, i, 0, isFillX)
        recur(heights, i, n - 1, isFillY)

    for j in range(n):
        recur(heights, 0, j, isFillX)
        recur(heights, m - 1, j, isFillY)

    res = []
    for i in range(m):
        for j in range(n):
            if isFillX[i][j] and isFillY[i][j]:
                res.append([i, j])
    return res


heights = [[1, 2, 2, 3, 5], [3, 2, 3, 4, 4], [2, 4, 5, 3, 1], [6, 7, 1, 4, 5], [5, 1, 1, 2, 4]]
res = pacificAtlantic(heights)
print(res)
```

#### [不用除法构建乘积数组](https://leetcode-cn.com/problems/gou-jian-cheng-ji-shu-zu-lcof/)

整体思路，**结果集中任何一个元素 = 其左边所有元素的乘积 * 其右边所有元素的乘积**。一轮循环构建左边的乘积并保存在结果集中，二轮循环 构建右边乘积的过程，乘以左边的乘积，并将最终结果保存

```python
class Solution:
    def constructArr(self, a: List[int]) -> List[int]:
        b, tmp = [1] * len(a), 1
        for i in range(1, len(a)):
            b[i] = b[i - 1] * a[i - 1] # 下三角
        for i in range(len(a) - 2, -1, -1):
            tmp *= a[i + 1]            # 上三角
            b[i] *= tmp                # 下三角 * 上三角
        return b

作者：jyd
链接：https://leetcode-cn.com/problems/gou-jian-cheng-ji-shu-zu-lcof/solution/mian-shi-ti-66-gou-jian-cheng-ji-shu-zu-biao-ge-fe/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```

## 链表相关算法考察：

**链表考察点：**链表的操作主要就是对指针的操作，常见面试题目都在考察指针的操作是否合理与正确。

**链表常见算法题：**

#### [反转链表](https://leetcode-cn.com/problems/reverse-linked-list/)

**java模板**

```java
class ListNode{
    int val;
    ListNode next;
    ListNode(int value){
        this.val = value;
    }
}
public class 反转链表 {
    public static void main(String[] args) {
        ListNode head = new ListNode(1);
        head.next = new ListNode(2);
        head.next.next = new ListNode(3);
        head.next.next.next = new ListNode(4);
        head.next.next.next.next = new ListNode(5);
        ListNode newHead = new 反转链表().reverseList2(head);
        while (newHead != null) {
            System.out.println(newHead.val);
            newHead = newHead.next;
        }
    }

    public ListNode reverseList(ListNode head) {
        ListNode pre = null;
        ListNode cur = head;
        while (cur != null) {
            ListNode next = cur.next;
            cur.next = pre;
            pre = cur;
            cur = next;
        }
        return pre;
    }

    public ListNode reverseList2(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode newHead = reverseList2(head.next);
        head.next.next = head;
        head.next = null;
        return newHead;
    }
}
```

**非递归反转：**

```java
class Solution:
    # 返回ListNode
    def ReverseList(self, pHead):
        pre = None
        cur = pHead
        while(cur):
            tem = cur.next
            cur.next = pre
            pre = cur
            cur = tem
        return pre
```

**递归反转链表**：

![img](https://labuladong.gitee.io/algo/images/%e5%8f%8d%e8%bd%ac%e9%93%be%e8%a1%a8/4.jpg)

```python
        if not head:return 
        if not head.next: return head
        node = self.reverseList(head.next)
        # head.next此时是已经反转的链表的最后一个元素
        head.next.next = head
        # 最后别忘了让最后一个元素指向为空
        head.next = None
        return node
```

**链表反转万能解法头插法：**模板：

```python 
		dummy = ListNode(0); dummy.next = head
        pre = dummy; cur= head
        while 1 :
        	# 删除p.next
            node = cur.next
            cur.next = cur.next.next
            # 插入到g的前面
            node.next = pre.next
            pre.next = node
        return dummy.next
```

**试水链表反转**

```python
		dummy = ListNode(0); dummy.next = head
        pre = dummy; cur= head
        length = 0
        while head:
            head = head.next
            length += 1
        for i in range(length-1):
            # 删除p.next
            node = cur.next
            cur.next = cur.next.next
            # 插入到g的前面
            node.next = pre.next
            pre.next = node
        return dummy.next
```

#### [反转链表区间](https://leetcode-cn.com/problems/reverse-linked-list-ii/)

- 链表在删除时大部分要用一个临时节点存下信息
- 凡是需要考虑左右边界的问题, 加个虚拟头节点准没错.
- **头插法**是链表反转的一把利刃

```python
class Solution:
    def reverseBetween(self, head: ListNode, left: int, right: int) -> ListNode:
        dummy = ListNode(0); dummy.next = head
        pre = dummy; cur= head
        for i in range(left-1):
            pre = pre.next
            cur = cur.next
        for i in range(right-left):
            # 删除p.next
            node = cur.next
            cur.next = cur.next.next
            # 插入到g的前面
            node.next = pre.next
            pre.next = node
        return dummy.next
```

#### [两两一组反转链表](https://leetcode-cn.com/problems/swap-nodes-in-pairs/)

```python
class Solution:
    def swapPairs(self, head: ListNode) -> ListNode:
        dummy = ListNode(0); dummy.next = head
        pre = dummy; cur = head
        while cur and cur.next:
            # 删除当前节点下一个并保存
            node = cur.next
            cur.next = cur.next.next
            # 将其迁移至pre 与 cur之间
            node.next = pre.next
            pre.next = node
            # 向前更新
            pre = cur
            cur = cur.next
        return dummy.next
```

#### [k个一组进行反转](https://leetcode-cn.com/problems/reverse-nodes-in-k-group/)

**注意内层循环是k-1次，不是k次**

```python
class Solution:
    def reverseKGroup(self, head: ListNode, k: int) -> ListNode:
        dummy = ListNode(0); dummy.next = head
        pre = dummy; cur= head
        length = 0
        while head:
            head = head.next
            length += 1
        for i in range(length//k):
            for j in range(k-1):
                # 删除p.next
                node = cur.next
                cur.next = cur.next.next
                # 插入到g的前面
                node.next = pre.next
                pre.next = node
            pre = cur
            cur = cur.next
        return dummy.next
```

java

```java
class Solution {
    public ListNode reverseKGroup(ListNode head, int k) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode pre = dummy, cur = head;
        int length = 0;
        while(head != null){
            length++;
            head = head.next;
        }
        for(int i = 0; i < length/k; i++){
            for(int j =0; j<k-1; j++){
                ListNode node = cur.next;
                cur.next = cur.next.next;
                node.next = pre.next;
                pre.next = node;
            }
            pre = cur;
            cur = cur.next;
        }
        return dummy.next;
    }
}
```

#### 合并有序单链表

```python
class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        dummy = ListNode()
        head = dummy
        while list1 and list2:
            if list1.val < list2.val:
                head.next = list1
                list1 = list1.next
            else:
                head.next = list2
                list2 = list2.next
            head = head.next
        head.next = list1 if list1 else list2
        return dummy.next
```

#### [找出单链表的中间节点](https://leetcode-cn.com/problems/middle-of-the-linked-list/)

要知道，如果循环条件里面有cur.next.next，不能只判断cur.next != null,而要判断`cur != null && cur.next != null`，因为虽然赋值的时候不会出问题，但是当cur为null时他是没有next的。

![image-20220405155248780](http://pic.wyydd.top/image-20220405155248780.png)

```java
class Solution {
    public ListNode middleNode(ListNode head) {
        ListNode pre = head, cur = head;
        while(cur != null && cur.next != null){
            pre = pre.next;
            cur = cur.next.next;
        }
        return pre;
    }
}
```

#### [判断链表有环](https://leetcode-cn.com/problems/linked-list-cycle/)

```python
class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        slow = head; fast = head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            if fast == slow: return True
        return False
```

java代码

```java
public class Solution {
    public boolean hasCycle(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;
        # 这里的判断比较关键
        while(fast != null && fast.next != null){
            slow = slow.next;
            fast = fast.next.next;
            if(fast == slow) return true;
        }
        return false;
    }
}
```

#### [找出进入环的第一个节点](https://leetcode-cn.com/problems/c32eOV/)

**快指针比慢指针多走了一个环，而路程是是慢指针的两倍，所以慢指针路程==环长度，假设相遇点距离起点为m,那么head距离入口也为m**

```python
class Solution:
    def detectCycle(self, head: ListNode) -> ListNode:
        slow = head; fast = head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            if slow == fast: break
        if not fast or not fast.next: return None
        slow = head
        while slow != fast:
            slow = slow.next
            fast = fast.next
        return slow
```

java

```java
public class Solution {
    public ListNode detectCycle(ListNode head) {
        ListNode pre = head, cur = head;
        while(cur != null && cur.next != null){
            pre = pre.next;
            cur = cur.next.next;
            if(pre == cur) break;
        }
        if (cur == null || cur.next == null) return null;
        pre = head;
        while(pre != cur){
            pre = pre.next;
            cur = cur.next;
        }
        return pre;
    }
}
```

#### [求单链表相交的第一个节点](https://leetcode-cn.com/problems/intersection-of-two-linked-lists/)

```python
class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> ListNode:
        A, B = headA, headB
        while A != B:
            A = A.next if A else headB
            B = B.next if B else headA
        return A
```

#### [重排链表](https://leetcode-cn.com/problems/reorder-list/)

~~~python
```
class Solution:
    def reorderList(self, head: ListNode) -> None:
        # 找到链表中间节点
        slow = head; fast = head
        while fast.next and fast.next.next:
            slow = slow.next
            fast = fast.next.next
    
    # 反转后半部分
    # 此时slow 是中界上半部分
        pre = None; cur = slow.next
        while cur:
            tem = cur.next
            cur.next = pre
            pre = cur
            cur = tem

        # print(pre)
        # print(head)
        # print(slow)

        # 这里很重要 如果slow下一个为空 等于切断 用第一种方法；
        # 如果等于pre 相当于接上用法二

        # 法1
        slow.next = None
        l1 = head; l2 = pre
        while l1 and l2:
            l1t = l1.next
            l2t = l2.next
            l2.next = l1.next
            l1.next = l2
            l1 = l1t
            l2 = l2t

        # 法2
        # slow.next = pre
        # l1 = head; l2 = slow.next
        # while l1 != slow :
        #     # 先把后面的续上 不然会丢掉
        #     slow.next = l2.next
        #     l2.next = l1.next
        #     l1.next = l2
        #     l1 = l2.next
        #     l2 = slow.next
~~~

#### [**链表的奇偶重排**](https://www.nowcoder.com/practice/02bf49ea45cd486daa031614f9bd6fc3?tpId=295&tags=&title=&difficulty=0&judgeStatus=0&rp=0&sourceUrl=)

- 双链表 一个指向head，一个指向head.next，改变链表指向即可
- 指向里有head.next.next，但是只是简单指向，无需让其赋值，认为其为null即可

```java
import java.util.*;
public class Solution {
    public ListNode oddEvenList (ListNode head) {
        if(head == null) return null;
        ListNode pre = head,  cur = head.next;
        ListNode res = cur;
        while(cur != null && cur.next != null){
            pre.next = cur.next;
            cur.next = cur.next.next;
            pre = pre.next;
            cur = cur.next;
        }
        pre.next = res;
        return head;
    }
}
```

#### [ 两个逆序链表生成相加链表](https://leetcode-cn.com/problems/add-two-numbers/)

```python
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        res = ListNode(0)
        t = res; carry = 0
        # 这里的 or carry 不能省略，防止最后一位有进位
        while l1 or l2 or carry:
            i1 = l1.val if l1 else 0
            i2 = l2.val if l2 else 0
            add = i1+i2+carry
            if add < 10:
                add = add
                carry = 0
            else:
                add = add-10
                carry = 1
            # add = add-10 if add>=10 else add
            # carry = 1 if add>=10 else 0
            res.next = ListNode(add)
            res = res.next
            if l1: l1 = l1.next
            if l2: l2 = l2.next
        return t.next
```

#### [两个链表生成相加链表](https://www.nowcoder.com/practice/c56f6c70fb3f4849bc56e33ff2a50b6b?tpId=117&&tqId=37814&rp=1&ru=/ta/job-code-high&qru=/ta/job-code-high/question-ranking)

```python
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        stk1,stk2 = [],[]
        while l1:
            stk1.append(l1.val)
            l1 = l1.next
        while l2:
            stk2.append(l2.val)
            l2 = l2.next
        carry,dummy = 0, ListNode(0)
        while stk1 or stk2 or carry:
            n1 = stk1.pop() if stk1 else 0
            n2 = stk2.pop() if stk2 else 0
            add = n1+n2+carry
            num = add-10 if add>=10 else add
            carry = 1 if add>=10 else 0
            cur = ListNode(num)
            cur.next = dummy.next
            dummy.next = cur
        return dummy.next
```

> 顺便扩展------加法题目
>
> 1. 「**加法**」系列题目都不难，其实就是 **「列竖式」模拟法** 。
> 2. 需要注意的是 `while`循环结束条件，注意遍历两个「加数」不要越界，以及考虑进位。

**66 给数组的最后一位加一**

```python
class Solution:
    def plusOne(self, digits: List[int]) -> List[int]:
        if not digits:return []
        carry = 1; res = []
        while digits or carry:
            num = digits.pop() if digits else 0
            add = num+carry
            carry = 1 if add>9 else 0
            add = add-10 if add>9 else add
            res.append(add)
        return res[::-1]
```

**67 二进制求和**

```python
class Solution:
    def addBinary(self, a: str, b: str) -> str:
        res = ""; i=len(a)-1; j = len(b)-1;carry=0
        while i>=0 or j>=0 or carry:
            a1 = int(a[i]) if i>=0 else 0
            b1 = int(b[j]) if j>=0 else 0
            add = a1+b1+carry
            carry = 1 if add>=2 else 0
            # add 有可能是3的哦 1+1+进位
            add = add-2 if add>=2  else add
            res += str(add)
            i -= 1; j -= 1
        return res[::-1]
```

#### [合并K个升序链表](https://leetcode-cn.com/problems/merge-k-sorted-lists/) 

```python
class Solution:
    def mergeKLists(self, lists: List[ListNode]) -> ListNode:
        import heapq
        dummy = ListNode(0)
        cur = dummy;heap = []
        for i in range(len(lists)):
            if lists[i]:
                heapq.heappush(heap, (lists[i].val, i))
                # 思考这里是否可以优化
                lists[i] = lists[i].next
        
        while heap:
            val,index = heapq.heappop(heap)
            cur.next = ListNode(val)
            cur = cur.next
            if lists[index]:
                heapq.heappush(heap,(lists[index].val,index))
                lists[index] = lists[index].next
        return dummy.next
```

#### [剑指 Offer 35. 复杂链表的复制](https://leetcode-cn.com/problems/fu-za-lian-biao-de-fu-zhi-lcof/)

```python
class Solution:
    def copyRandomList(self, head: 'Node') -> 'Node':
        if not head: return
        cur = head
        # 1. 复制各节点，并构建拼接链表
        while cur:
            tmp = Node(cur.val)
            tmp.next = cur.next
            cur.next = tmp
            cur = tmp.next
        # 2. 构建各新节点的 random 指向
        cur = head
        while cur:
            if cur.random:
                cur.next.random = cur.random.next
            cur = cur.next.next
        # 3. 拆分两链表
        cur = res = head.next
        pre = head
        while cur.next:
            pre.next = pre.next.next
            cur.next = cur.next.next
            pre = pre.next
            cur = cur.next
        pre.next = None # 单独处理原链表尾节点
        return res      # 返回新链表头节点
```

#### [删除排序链表中的重复元素](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list/)

python

```python
class Solution:
    def deleteDuplicates(self, head: ListNode) -> ListNode:
        res = head
        while(res and res.next):
            if res.val == res.next.val: res.next = res.next.next
            else: res = res.next
        return head
```

java

```java
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        ListNode cur = head;
        while(cur != null && cur.next != null){
            if(cur.val == cur.next.val) cur.next = cur.next.next;
            else cur = cur.next;
        }
        return head;
    }
}
```

#### [删除排序链表中的重复元素 II](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list-ii/)

**核心其实就是用一个中间变量不停迭代找出重复元素的中止位置**

#####  迭代解法
```python
class Solution:
    def deleteDuplicates(self, head: ListNode) -> ListNode:
        dummy = ListNode(0)
        dummy.next = head
        cur = dummy
        while cur.next and cur.next.next:
            if cur.next.val == cur.next.next.val:
                tem = cur.next
                while tem and cur.next and tem.val == cur.next.val:
                    tem = tem.next
                cur.next = tem
            else: cur = cur.next
        return dummy.next
```

#####  递归解法

```python
# 删除以 head 作为开头的有序链表中，值出现重复的节点。
        if not head or not head.next:
            return head
        if head.val != head.next.val:
            head.next = self.deleteDuplicates(head.next)
        else:
            move = head.next
            while move and head.val == move.val:
                move = move.next
            return self.deleteDuplicates(move)
        return head
```

## 二叉树相关算法考察：

**二叉树常见算法题：**

#### [分层遍历（宽度优先遍历）](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/)

**java模板**

```java
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) { val = x; }
}

public class levelOrder102 {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<>();
        if (root == null) {
            return result;
        }
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        queue.offer(root);
        while (!queue.isEmpty()) {
            int size = queue.size();
            List<Integer> list = new ArrayList<Integer>();
            for (int i = 0; i < size; i++) {
                TreeNode node = queue.poll();
                list.add(node.val);
                if (node.left != null) {
                    queue.offer(node.left);
                }
                if (node.right != null) {
                    queue.offer(node.right);
                }
            }
            result.add(list);
        }
        return result;
    }

    public static void main(String[] args) {
        TreeNode root = new TreeNode(3);
        TreeNode left = new TreeNode(9);
        TreeNode right = new TreeNode(20);
        TreeNode left1 = new TreeNode(15);
        TreeNode right1 = new TreeNode(7);
        root.left = left;
        root.right = right;
        left.left = left1;
        left.right = right1;
        levelOrder102 levelOrder102 = new levelOrder102();
        List<List<Integer>> result = levelOrder102.levelOrder(root);
        for (List<Integer> list : result) {
            for (Integer i : list) {
                System.out.print(i + " ");
            }
            System.out.println();
        }
    }
}
```

**python代码**

```python
class Solution:
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        if not root: return []
        res, queue = [], collections.deque()
        queue.append(root)
        while queue:
            tmp = []
            for _ in range(len(queue)):
                node = queue.popleft()
                tmp.append(node.val)
                if node.left: queue.append(node.left)
                if node.right: queue.append(node.right)
            res.append(tmp[::-1] if len(res) % 2 else tmp)
        return res
```

#### [二叉树的右视图](https://leetcode-cn.com/problems/binary-tree-right-side-view/)

```python
class Solution:
    def rightSideView(self, root: TreeNode) -> List[int]:
        if not root: return []
        queue = []; res =[]
        queue.append(root)
        while queue:
            for i in range(len(queue)):
                node = queue.pop(0)
                if node.left: queue.append(node.left)
                if node.right: queue.append(node.right)
            res.append(node.val)
        return res
```

#### 前序遍历，中序遍历，后序遍历

递归写法太简单，以下是非递归写法



```python
class Solution:
    def inorderTraversal(self, root: TreeNode) -> List[int]:
        stack = [(0,root)]
        res = []
        while stack:
            visited,node = stack.pop()
            if not node: continue
            if not visited:
                stack.append((0,node.right))
                stack.append((1,node))
                stack.append((0,node.left))
            else: res.append(node.val)
        return res
```

![图片](https://mmbiz.qpic.cn/mmbiz_jpg/liaT5dytkaTfrDKKBt1SMHeJL6qDia4CLbSayGer6vIH5axVSiciawBfDI7CyYuiaUN1tofQrFBtFxDppAH6PO8UboQ/640?wx_fmt=jpeg&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

#### [求二叉树的深度](https://leetcode-cn.com/problems/er-cha-shu-de-shen-du-lcof/)

```java
class Solution:
    def maxDepth(self, root: TreeNode) -> int:
        if not root: return 0
        return max(self.maxDepth(root.left), self.maxDepth(root.right)) + 1
```

#### [判断两颗二叉树是否是相同的树](https://leetcode-cn.com/problems/same-tree/solution/)

```python
class Solution:
    def isSameTree(self, p: TreeNode, q: TreeNode) -> bool:
        if not p and not q: return True
        if not p or not q: return False
        return p.val == q.val and self.isSameTree(p.left,q.left) and self.isSameTree(p.right,q.right)
```

#### [对称的二叉树](https://leetcode-cn.com/problems/dui-cheng-de-er-cha-shu-lcof/)

```python
class Solution:
    def isSymmetric(self, root: TreeNode) -> bool:
        def recur(L, R):
            if not L and not R: return True
            if not L or not R or L.val != R.val: return False
            return recur(L.left, R.right) and recur(L.right, R.left)

        return recur(root.left, root.right) if root else True
```

#### [剑指 Offer 26. 树的子结构](https://leetcode-cn.com/problems/shu-de-zi-jie-gou-lcof/)

$$
递归函数定义：以n_A为根节点的子树是否包含树B
$$

```java
class Solution {
    public boolean isSubStructure(TreeNode A, TreeNode B) {
        if(A == null || B == null) return false;
        return recur(A,B) || isSubStructure(A.left,B) || isSubStructure(A.right,B);
    }

    public boolean recur(TreeNode A, TreeNode B){
        if(B == null) return true;
        if(A == null) return false;
        return (A.val == B.val) && recur(A.left,B.left) && recur(A.right,B.right);
    }
}
```

```python
class Solution:
    def isSubStructure(self, A: TreeNode, B: TreeNode) -> bool:
        def recur(a,b):
            # 必须先判断b
            if not b: return True
            if not a: return False
            return a.val == b.val and recur(a.left,b.left) and recur(a.right,b.right)
        if not A or not B: return False
        return recur(A,B) or self.isSubStructure(A.left,B) or self.isSubStructure(A.right,B
```

#### [二叉搜索树的最近公共祖先](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-zui-jin-gong-gong-zu-xian-lcof/)

```python
class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        while root:
            if root.val < p.val and root.val < q.val:root = root.right
            elif root.val >p.val and root.val >q.val: root = root.left
            else: break
        return root
```

#### [求二叉树中两个节点的最低公共祖先节点](https://leetcode-cn.com/problems/er-cha-shu-de-zui-jin-gong-gong-zu-xian-lcof/)

```python 
class Solution:
    def lowestCommonAncestor(self, root: TreeNode, p: TreeNode, q: TreeNode) -> TreeNode:
        if not root: return None
        if root == p or root == q: return root
        left = self.lowestCommonAncestor(root.left,p,q)
        right = self.lowestCommonAncestor(root.right,p,q)
        if not left and not right: return None
        if right and  left: return root
        return left if left else right
```

java代码

```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        // base case
        if(root == null) return null;
        if(root == p || root == q) return root;
        // 递归调用
        TreeNode left = lowestCommonAncestor(root.left,p,q);
        TreeNode right = lowestCommonAncestor(root.right,p,q);
        // 分情况讨论
        if(left != null && right != null) return root;
        if(left == null && right == null) return null;
        return left != null?left:right;
    }
}
```

#### [重建二叉树](https://leetcode-cn.com/problems/zhong-jian-er-cha-shu-lcof/)

- 给**中序遍历**建立哈希
- 递归中止条件是**il>ir or pl>pr**
- 根据索引-il求出**左子树大小**
- 递归关键：注意**下次遍历要加一** 和 **preorder左树边界**是pl+leftsize，其他的好推

```
root.left = self.recur(preorder,pl+1,pl+leftsize,inorder,il,index-1)
root.right = self.recur(preorder,pl+leftsize+1,pr,inorder,index+1,ir)
```

```python
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> TreeNode:
        return self.recur(preorder,0,len(preorder)-1,inorder,0,len(inorder)-1)
    def recur(self,preorder,pl,pr,inorder,il,ir):
        hmap = dict()
        for i,val in enumerate(inorder):
            hmap[val] = i
            # 1 base case 两个边界都可以用来判断
        if il > ir or pl > pr:return
        root = TreeNode(preorder[pl])
        index = hmap[preorder[pl]]
        leftsize = index-il
        # 2 前序遍历的左侧边界不要只加了leftsize而忘了加上pl
        root.left = self.recur(preorder,pl+1,pl+leftsize,inorder,il,index-1)
        root.right = self.recur(preorder,pl+leftsize+1,pr,inorder,index+1,ir)
        return root
```

#### [路径总和](https://leetcode-cn.com/problems/path-sum/)

```python
class Solution:
    def hasPathSum(self, root: Optional[TreeNode], targetSum: int) -> bool:
        if not root:return False
        if not root.left and not root.right:
            if root.val == targetSum: return True
        return self.hasPathSum(root.left,targetSum-root.val) or self.hasPathSum(root.right,targetSum-root.val)
```

java代码

```java
class Solution {
    public boolean hasPathSum(TreeNode root, int sum) {
        if (root == null) {
            return false;
        }
        if (root.left == null && root.right == null) {
            return sum == root.val;
        }
        return hasPathSum(root.left, sum - root.val) || hasPathSum(root.right, sum - root.val);
    }
}
```

这两道题告诉我 如果是回溯法，判断root 不为空也是非常重要的

#### [剑指 Offer 34. 二叉树中和为某一值的路径](https://leetcode-cn.com/problems/er-cha-shu-zhong-he-wei-mou-yi-zhi-de-lu-jing-lcof/)

```python
class Solution:
    def pathSum(self, root: TreeNode, sum: int) -> List[List[int]]:
        res, path = [], []
        def recur(root, tar):
            # 这一步也不能省略，这是在其他情况下的返回，不然会报 root NoneType的错
            if not root: return
            path.append(root.val)
            tar -= root.val
            if tar == 0 and not root.left and not root.right: 
                res.append(list(path))
            recur(root.left, tar)
            recur(root.right, tar)
           # 回溯，清理现场
            path.pop()
            
        recur(root, sum)
        return res
    
# 方法二 我的方法
class Solution:
    def pathSum(self, root: Optional[TreeNode], targetSum: int) -> List[List[int]]:
        if not root: return []
        res,tem = [],[]
        def dfs(root,targetSum,tem):
            if not root : return
            if not root.left and not root.right:
                if targetSum == root.val:
                    tem.append(root.val)
                    res.append(tem[:])
                    tem.pop()
                return
            tem.append(root.val)
            dfs(root.left,targetSum-root.val,tem)
            dfs(root.right,targetSum-root.val,tem)
            tem.pop()
        dfs(root,targetSum,tem)
        return res
```

#### [二叉树中的最大路径和](https://leetcode-cn.com/problems/binary-tree-maximum-path-sum/)

核心在于计算结果的时候要计算左右子树，递归返回的时候只能返回较大的一边

```python
class Solution:
    def maxPathSum(self, root: Optional[TreeNode]) -> int:
        # 定义：计算从根节点 root 为起点的最大单边路径和
        def oneSideMax(root):
            if not root: return 0
            leftmax = max(0,oneSideMax(root.left))
            rightmax = max(0,oneSideMax(root.right))
            self.res = max(self.res,root.val+leftmax+rightmax)
            return root.val+max(leftmax,rightmax)
        self.res = -float("inf")
        oneSideMax(root)
        return self.res
```

#### [二叉树的直径](https://leetcode-cn.com/problems/diameter-of-binary-tree/)

- 遍历每一个节点，以每一个节点为中心点计算最长路径（左子树边长+右子树边长），更新全局变量max。
- 灵活运用二叉树的后序遍历，在 `maxDepth` 的后序遍历位置顺便计算最大直径
- 直径是边长和 不是节点数

```python
class Solution:
    def diameterOfBinaryTree(self, root: TreeNode) -> int:
        def maxDepth(root):
            if not root: return 0
            leftl = maxDepth(root.left)
            rightl = maxDepth(root.right)
            self.res = max(self.res,leftl+rightl)
            return 1 + max(leftl,rightl)
        self.res = 0
        maxDepth(root)
        return self.res
```

#### [验证二叉搜索树](https://leetcode-cn.com/problems/validate-binary-search-tree/) 

![img](https://pic.leetcode-cn.com/30fc2cf46bd2af2c63583a0e3b7b463ecf999560edac55a1e12f20b805ac3c13-%E9%AA%8C%E8%AF%81%E4%BA%8C%E5%8F%89%E6%90%9C%E7%B4%A2%E6%A0%91.png)

```python
class Solution:
    def isValidBST(self, root: TreeNode) -> bool:
        def isBST(root, min_val, max_val):
            if root == None:
                return True
            # print(root.val)
            if root.val >= max_val or root.val <= min_val:
                return False
            return isBST(root.left, min_val, root.val) and isBST(root.right, root.val, max_val)
        return isBST(root, float("-inf"), float("inf"))
```

#### [ 二叉搜索树的第k大节点](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-di-kda-jie-dian-lcof/)

核心是维护一个全局变量self.k 和 self.res

```python
class Solution:
    def kthLargest(self, root: TreeNode, k: int) -> int:
        def dfs(root):
            if not root: return
            dfs(root.right)
            if self.k == 0: return
            self.k -= 1
            if self.k == 0: self.res = root.val
            dfs(root.left)
        self.k = k
        dfs(root)
        return self.res
```

#### [剑指 Offer 33. 二叉搜索树的后序遍历序列](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-hou-xu-bian-li-xu-lie-lcof/)

思路：数组最后一个数为root，小于root的为左子树，大于root的为右子树，对于左右子树的序列亦是如此。

解法1：递归判断，满足条件才返回true

```python
class Solution:
    def verifyPostorder(self, postorder: List[int]) -> bool:
        def recur(i,j):
            # base case: 必须要有
            if i >= j: return True
            p = i 
            while postorder[p] < postorder[j]: p += 1
            m = p 
            while postorder[p] > postorder[j]: p += 1
            # 注意：m是大于arr[j]的，因此右子树是从m到 *j-1*
            return p == j and recur(i,m-1) and recur(m,j-1)  
        return recur(0,len(postorder)-1)
```

解法2：[辅助单调栈](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-hou-xu-bian-li-xu-lie-lcof/solution/mian-shi-ti-33-er-cha-sou-suo-shu-de-hou-xu-bian-6/)，还没看

#### [剑指 Offer 36. 二叉搜索树与双向链表](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-yu-shuang-xiang-lian-biao-lcof/)

**算法流程：**

**`dfs(cur):`** 递归法中序遍历；

1. **终止条件：** 当节点 `cur` 为空，代表越过叶节点，直接返回；
2. 递归左子树，即 `dfs(cur.left)` ；
3. 构建链表：
   1. **当 `pre` 为空时：** 代表正在访问链表头节点，记为 `head` ；
   2. **当 `pre` 不为空时：** 修改双向节点引用，即 `pre.right = cur` ， `cur.left = pre` ；
   3. **保存 `cur` ：** 更新 `pre = cur` ，即节点 `cur` 是后继节点的 `pre` ；
4. 递归右子树，即 `dfs(cur.right)` ；

```python
class Solution:
    def treeToDoublyList(self, root: 'Node') -> 'Node':
        def dfs(cur):
            if not cur: return
            dfs(cur.left) # 递归左子树
            if self.pre: # 修改节点引用
                self.pre.right, cur.left = cur, self.pre
            else: # 记录头节点
                self.head = cur
            self.pre = cur # 保存 cur
            dfs(cur.right) # 递归右子树
        
        if not root: return
        self.pre = None
        dfs(root)
        self.head.left, self.pre.right = self.pre, self.head
        return self.head
```

#### [剑指 Offer 37. 序列化二叉树](https://leetcode-cn.com/problems/xu-lie-hua-er-cha-shu-lcof/)

```python
class Codec:

    def serialize(self, root):
        if not root:
            return '#_'
        res = str(root.val) + '_' 
        res += str(self.serialize(root.left)) 
        res += str(self.serialize(root.right)) 
        return res
        
    def deserialize(self, data):
        def reconPreOrder(queue):
            value = queue.pop(0)
            if value == '#':
                return None
            head = TreeNode(int(value))
            head.left = reconPreOrder(queue)
            head.right = reconPreOrder(queue)
            return head
        queue = data.split('_')
        return reconPreOrder(queue)
```

在算法题目的考察中，不光将队列和堆栈做为辅助数据结构考察，还会直接对其相关特性进行考察，典型的算法题目如下：

## 堆栈与队列

#### [包含min函数的栈](https://leetcode-cn.com/problems/bao-han-minhan-shu-de-zhan-lcof/)

**算法思路：**

我们考虑增加一个专门用来存储min值的辅助栈。
增加是 如果辅助栈为空 或者 新元素小于辅助栈栈顶元素，则加入栈顶
取出时 如果普通栈元素等于辅助栈栈顶元素，则辅助栈一起出栈


**实现步骤：**

- 比如，data依次入栈：5, 4, 3, 8, 10, 11, 12, 1。则辅助栈依次入栈：5, 4, 3，no，no, no, no, 1。其中，no代表此次不入栈。也就是说每次入栈的时候，如果入栈的元素比min中的栈顶元素小或等于则入栈，否则不入栈。
- 当出栈的时候，我们比较辅助栈与当前出栈的值是否相等。如果相等，则辅助栈栈顶元素也需要出栈。
- 当需要获取栈中最小元素的时候，我们直接获取到辅助栈的栈顶元素即可。
- 这里需要注意的是，在获取栈中的min值时，我们应该使用minStack.peek方法而不是minStack.pop方法。peek方法仅仅是获取数值，但是pop方法则会执行出栈操作。

```python
class MinStack:
    def __init__(self):
        self.A, self.B = [], []

    def push(self, x: int) -> None:
        self.A.append(x)
        # 此处必须是小于等于
        if not self.B or self.B[-1] >= x:
            self.B.append(x)

    def pop(self) -> None:
        if self.A.pop() == self.B[-1]:
            self.B.pop()

    def top(self) -> int:
        return self.A[-1]

    def min(self) -> int:
        return self.B[-1]
```
java 代码
```java
class MinStack {
    Stack<Integer> stack1;
    Stack<Integer> stack2; // 这个是辅助的最小栈
    
    /** initialize your data structure here. */
    public MinStack() {
        stack1 = new Stack<>();
        stack2 = new Stack<>();
    }
    
    public void push(int x) {
        stack1.push(x);
        if(stack2.isEmpty() || x <= stack2.peek()) stack2.push(x);
    }
    
    public void pop() {
//        这里千万不要用 if (stack1.pop() == stack2.peek())
//        因为java这里比较的是对象地址 而不是值
        if (stack1.pop().equals(stack2.peek())) {
            stack2.pop();
        }
    }
    
    public int top() {
        return stack1.peek();
    }
    
    public int min() {
        return stack2.peek();
    }
}
```
#### [有效的括号](https://leetcode-cn.com/problems/valid-parentheses/)
```java
class Solution {
    public boolean isValid(String s) {
        Map<Character, Character> map = new HashMap<>();
        map.put('(',')');
        map.put('{', '}');
        map.put('[', ']');
        map.put('?', '?');
        Stack<Character> stack = new Stack<>();
        stack.push('?');
        for (Character c : s.toCharArray()) {
//            假如 输入为"([)]" 当)入栈以后，是存在其不在key里面的风险的
//            虽然对于java其会返回null,不会抛异常
            if (map.containsKey(stack.peek()) &&  c == map.get(stack.peek())) {
                stack.pop();
            } else {
                stack.push(c);
            }
        }
        return stack.size() == 1;
    }
}
```
python解法
```python
class Solution:
    def isValid(self, s: str) -> bool:
        dic = {'{': '}',  '[': ']', '(': ')','?':'?'}
        stk = ['?']
        for i in range(len(s)):
            if s[i] in dic:stk.append(s[i])
            # else: return s[i]==dic[stk.pop()]
            elif dic[stk.pop()] != s[i]: return False 
        return len(stk)==1
```
```python
class Solution:
    def isValid(self, s: str) -> bool:
        dic = {'{': '}',  '[': ']', '(': ')','?':'?'}
        stack = ['?']
        for c in s:
            if c == dict[stack[-1]]: stack.pop()
            else: stack.append(c)
        return len(stack)==1
```

#### [用两个栈实现队列](https://www.nowcoder.com/practice/54275ddae22f475981afa2244dd448c6?tpId=117&&tqId=37774&rp=1&ru=/ta/job-code-high&qru=/ta/job-code-high/question-ranking)
代码虽长，题很简单，就是要注意peek 和 pop 函数都需要stack2掏空再下结论。
```java
class MyQueue {
    Stack<Integer> stack1;
    Stack<Integer> stack2;

    public MyQueue() {
        stack1 = new Stack<>();
        stack2 = new Stack<>();
    }
    
    public void push(int x) {
        stack2.push(x);
    }
    
    public int pop() {
        if (stack1.isEmpty()) {
            while (!stack2.isEmpty()) {
                stack1.push(stack2.pop());
            }
        }
        return stack1.pop();
    }
    
    public int peek() {
        if (stack1.isEmpty()) {
            while (!stack2.isEmpty()) {
                stack1.push(stack2.pop());
            }
        }
        return stack1.peek();
    }
    
    public boolean empty() {
        return stack1.isEmpty() && stack2.isEmpty();
    }
}
```
pyhton 解法
```python
class Solution:
    def __init__(self):
        self.stake1 = []
        self.stake2 = []
    
    def push(self, node):
        self.stake1.append(node)
        
    def pop(self):
#         1 必须2不空1才出栈，这一步很关键
        if(not self.stake2):
        # 2 导数据则必须一次性倒完
            while(self.stake1):
                self.stake2.append(self.stake1.pop())
        if(self.stake2): return self.stake2.pop()
        else: return -1
```

#### [用两个队列实现栈](https://leetcode-cn.com/problems/implement-stack-using-queues/)
- 对于queue1 queue2在类内定义成全局类变量
- push 是关键代码，就是新进来先放到queue这个框子里，然后把主队列依次取出
- 也放到框子里，这样，就可以保证 比较新的元素一直在队列的前面
- 不过为了方便后面操作，queue1 queue2交换，可以一直维持这个算法规则
```java
class MyStack {
    Queue<Integer> queue1;
    Queue<Integer> queue2;

    public MyStack() {
        queue1 = new LinkedList<>();
        queue2 = new LinkedList<>();
    }
    public void push(int x) {
        queue2.offer(x);
        while (!queue1.isEmpty()) {
            queue2.offer(queue1.poll());
        }
        Queue<Integer> tem = queue1;
        queue1 = queue2;
        queue2 = tem;
    }
    
    public int pop() {
        return queue1.poll();
    }
    
    public int top() {
        return queue1.peek();
    }
    
    public boolean empty() {
        return queue1.isEmpty();
    }
}

```
python 解法
```python
class MyStack:

    def __init__(self):
        self.queue1 = collections.deque()
        self.queue2 = collections.deque()

    def push(self, x: int) -> None:
        #有了新元素，先放到辅助队列，再将主队列依次放入辅助队列并保持主副关系，实现后进先出
        self.queue2.append(x)
        while self.queue1:
            self.queue2.append(self.queue1.popleft())
        self.queue1, self.queue2 = self.queue2, self.queue1

    def pop(self) -> int:
        return self.queue1.popleft()
```

#### [LRU 缓存机制](https://leetcode-cn.com/problems/lru-cache/)

![HashLinkedList](https://pic.leetcode-cn.com/b84cf65debb43b28bd212787ca63d34c9962696ed427f638763be71a3cb8f89d.jpg)

**为什么要是双向链表，单链表行不行？另外，既然哈希表中已经存了 key，为什么链表中还要存键值对呢，只存值不就行了？**

```python
class ListNode:
    # 初始化key value 默认为NONE
    def __init__(self, key=None, value=None):
        self.key = key
        self.value = value
        self.prev = None
        self.next = None


class LRUCache:
    def __init__(self, capacity: int):
        self.capacity = capacity
        self.hashmap = {}
        # 新建两个节点 head 和 tail
        self.head = ListNode()
        self.tail = ListNode()
        # 初始化链表为 head <-> tail
        self.head.next = self.tail
        self.tail.prev = self.head

    # 因为get与put操作都可能需要将双向链表中的某个节点移到末尾，所以定义一个方法
    def move_node_to_tail(self, key):
            # 先将哈希表key指向的节点拎出来，为了简洁起名node
            #      hashmap[key]                               hashmap[key]
            #           |                                          |
            #           V              -->                         V
            # prev <-> node <-> next         pre <-> next   ...   node
            node = self.hashmap[key]
            node.prev.next = node.next
            node.next.prev = node.prev
            # 之后将node插入到尾节点前
            #                 hashmap[key]                 hashmap[key]
            #                      |                            |
            #                      V        -->                 V
            # prev <-> tail  ...  node                prev <-> node <-> tail
            node.prev = self.tail.prev
            node.next = self.tail
            self.tail.prev.next = node
            self.tail.prev = node

    def get(self, key: int) -> int:
        if key in self.hashmap:
            # 如果已经在链表中了久把它移到末尾（变成最新访问的）
            self.move_node_to_tail(key)
        res = self.hashmap.get(key, -1)
        if res == -1:
            return res
        else:
            return res.value

    def put(self, key: int, value: int) -> None:
        if key in self.hashmap:
            # 如果key本身已经在哈希表中了就不需要在链表中加入新的节点
            # 但是需要更新字典该值对应节点的value
            self.hashmap[key].value = value
            # 之后将该节点移到末尾
            self.move_node_to_tail(key)
        else:
            if len(self.hashmap) == self.capacity:
                # 去掉哈希表对应项
                self.hashmap.pop(self.head.next.key)
                # 去掉最久没有被访问过的节点，即头节点之后的节点
                self.head.next = self.head.next.next
                self.head.next.prev = self.head
            # 如果不在的话就插入到尾节点前
            new = ListNode(key, value)
            self.hashmap[key] = new
            new.prev = self.tail.prev
            new.next = self.tail
            self.tail.prev.next = new
            self.tail.prev = new
```

java 自带函数版 linkedHashMap
```java
class LRUCache {
    int cap;
    LinkedHashMap<Integer, Integer> cache = new LinkedHashMap<>();
    public LRUCache(int capacity) {
        this.cap = capacity;
    }

    public int get(int key) {
        if (!cache.containsKey(key)) {
            return -1;
        }
        // 将 key 变为最近使用
        makeRecently(key);
        return cache.get(key);
    }

    public void put(int key, int val) {
        if (cache.containsKey(key)) {
            // 修改 key 的值
            cache.put(key, val);
            // 将 key 变为最近使用
            makeRecently(key);
            return;
        }

        if (cache.size() >= this.cap) {
            // 链表头部就是最久未使用的 key
            int oldestKey = cache.keySet().iterator().next();
            cache.remove(oldestKey);
        }
        // 将新的 key 添加链表尾部
        cache.put(key, val);
    }

    private void makeRecently(int key) {
        int val = cache.get(key);
        // 删除 key，重新插入到队尾
        cache.remove(key);
        cache.put(key, val);
    }
}
```
java 手动实现版
```java
class LRUCache {
    
    class ListNode {
        int key;
        int value;
        ListNode prev;
        ListNode next;

        public ListNode(int key, int value) {
            this.key = key;
            this.value = value;
            this.prev = null;
            this.next = null;
        }

        public ListNode(int key, int value, ListNode pre, ListNode next) {
            this.key = key;
            this.value = value;
            this.prev = pre;
            this.next = next;
        }
    }


    int capacity = 0;
    Map<Integer, ListNode> map;
    ListNode dummyHead;
    ListNode dummyTail;

    public LRUCache(int capacity) {
        this.capacity = capacity;
        map = new HashMap<>();
        dummyHead = new ListNode(-1, -1);
        dummyTail = new ListNode(-1, -1);
        dummyHead.next = dummyTail;
        dummyTail.prev = dummyHead;
    }

    // time: O(1)
    public void put(int key, int value) {
        ListNode node = map.get(key);
        if (node != null) {
            node.value = value;
            moveNodeToHead(node);
        } else {
            ListNode newNode = new ListNode(key, value);
            if (map.size() == capacity) {
                ListNode delNode = removeTail();
                map.remove(delNode.key);
            }

            addToHead(newNode);
            map.put(key, newNode);
        }
    }

    // time: O(1)
    public int get(int key) {
        ListNode node = map.get(key);
        if (node != null) {
            moveNodeToHead(node);
            return node.value;
        }

        return -1;
    }

    public void moveNodeToHead(ListNode node) {
        removeFromList(node);
        addToHead(node);
    }

    public void addToHead(ListNode node) {
        node.prev = dummyHead;
        node.next = dummyHead.next;
        dummyHead.next.prev = node;
        dummyHead.next = node;
    }

    public void removeFromList(ListNode node) {
        ListNode tempPre = node.prev;
        ListNode tempNext = node.next;
        tempPre.next = tempNext;
        tempNext.prev = tempPre;
    }

    public ListNode removeTail() {
        ListNode tail = dummyTail.prev;
        removeFromList(tail);
        return tail;
    }
}
```
#### [单调队列：滑动窗口最大值](https://leetcode-cn.com/problems/sliding-window-maximum/)

**滑动窗口是一个从左到右的递减序列**
- 使用java方法的话自己维护以为大小为k的deque,在循环的过程中按顺序维护以下算法步骤
- 如果i>=k and i-窗口最左侧的值 >= k,说明值太旧了，得出栈
- 然后在滑动的过程中只要有更年轻，更强的元素出现，那栈尾元素都出栈，最后再将其插入栈尾
- 最后如果 i > k-1 了，说明可以存结果了，将栈内存活的最大值，也即栈头元素对应的数值存入结果集即可
```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        if(nums.length == 0) return new int[0];
        Deque<Integer> deque = new LinkedList<>();
        int[] res = new int[nums.length - k + 1];
        for (int i = 0; i < nums.length; i++) {
            if(i >= k && i-deque.peekFirst() >= k) deque.pollFirst();
            while (!deque.isEmpty() && nums[i] > nums[deque.peekLast()]) {
                deque.pollLast();
            }
            deque.offerLast(i);
            if(i >= k-1) res[i - k + 1] = nums[deque.peekFirst()];
        }
        return res;
    }
}
```
```python
class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        if not nums:return[]
        queue,res = [],[]
        for i in range(len(nums)):
            if i >= k and i-queue[0] >= k:queue.pop(0)
            while queue and nums[queue[-1]] < nums[i]:
                queue.pop()
            queue.append(i)
            if i >= k-1: res.append(nums[queue[0]])
        return res
```

我的low 解法

```Python
class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        res = []
        queue = [0]
        for i in range(1,k):
            while queue and nums[i] >= nums[queue[-1]]: queue.pop()
            queue.append(i)
        res.append(nums[queue[0]])
        for i in range(k,len(nums)):
            while queue and i - k >= queue[0]: queue.pop(0)
            while queue and nums[i] >= nums[queue[-1]]: queue.pop()
            queue.append(i)
            res.append(nums[queue[0]])
        return res
```

#### [单调栈：每日温度](https://leetcode-cn.com/problems/daily-temperatures/)

**倒序遍历，碰到干不过的就自动退位，栈顶元素自认记录当前大于i的第一个元素**

stack 从顶向下越来越大，如果栈顶元素干不过当前温度，那要退出，因为他是夹在中间的矮个子没啥存在的意义，但如果干得过，那栈顶就是第一个大于当前温度的，求结果加入结果集

```python
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        if not temperatures:return []
        stack,res = [],[0]*len(temperatures)
        for i in range(len(temperatures)-1,-1,-1):
            while stack and temperatures[stack[-1]] <= temperatures[i]:
                stack.pop()
            res[i] = stack[-1]-i if stack else 0
            stack.append(i)
        return res
```
java解法
```java
class Solution {
    public int[] dailyTemperatures(int[] temperatures) {
        if(temperatures.length == 0) return new int[0];
        Stack<Integer> stack = new Stack<>();
        int[] res = new int[temperatures.length];
        for (int i = temperatures.length - 1; i >= 0; i--) {
            while (!stack.isEmpty() && temperatures[i] >= temperatures[stack.peek()]) {
                stack.pop();
            }
            res[i] = stack.isEmpty() ? 0 : stack.peek() - i;
            stack.push(i);
        }
        return res;
    }
}
```
> **总结：**其实单调队列和单调栈没啥区别，就是看逆序遍历还是顺序遍历。而**单调队列和优先队列的区别**在于：单调队列是通过实时对比和剔除加入来保持元素的有序，而优先队列是自己调整内部元素来保持有序，是通过红黑树或者斐波那契堆来实现的。

以下是一道不典型的优先队列或者说小根堆来例题

703 数据流的第K大元素

![image-20210611180122505](E:\nutstore\md\javaInterview\README.assets\image-20210611180122505.png)

## 字符串相关算法：

在开始交流字符串面试题目之前，我们先来简单介绍下**子串和子序列的区别**吧。

1. **子串**：字符串中任意个**连续的字符**组成的子序列。
2. **子序列**：字符串中**按照前后顺序**取出的任意个字符组成，**不要求连续**。

#### [20. 有效的括号](https://leetcode-cn.com/problems/valid-parentheses/)

**括号问题每一个右括号都必须有一个与之匹配的左括号，因此一般用栈，左括号入栈，碰到右括号了做选择**

```python
class Solution:
    def isValid(self, s: str) -> bool:
        dic = {'{': '}',  '[': ']', '(': ')','?':'?'}
        stk = ['?']
        for i in range(len(s)):
            if s[i] in dic:stk.append(s[i])
            # else: return s[i]==dic[stk.pop()]
            elif dic[stk.pop()] != s[i]: return False 
        return len(stk)==1
```

#### [使括号有效的最少添加](https://leetcode-cn.com/problems/minimum-add-to-make-parentheses-valid/)
- 括号联想栈，左括号入栈，右括号出栈，如果没得出，说明缺少左括号，res++
- 最后查看栈内剩余元素，代表右括号缺少数目
- 借用该思想，用need记录需要的右括号数，可以优化空间复杂度

java丑陋写法
```java
class Solution {
    public int minAddToMakeValid(String s) {
        int res = 0, need = 0;
        for (char d : s.toCharArray()) {
            if (d == '(') {
                need++;
            } else {
                if (need == -1) {
                    res++;
                    need = 0;
                } else if (need == 0) {
                    res++;
                } else {
                    need--;
                }
            }
        }
        return need+res;
    }
}
```
优化写法带注释
```java
class Solution {
    public int minAddToMakeValid(String s) {
        // res 记录插入次数
        int res = 0;
        // need 变量记录右括号的需求量
        int need = 0;
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == '(') {
                // 对右括号的需求 + 1
                need++;
            }
            if (s.charAt(i) == ')') {
                // 对右括号的需求 - 1
                need--;
                if (need == -1) {
                    need = 0;
                    // 需插入一个左括号
                    res++;
                }
            }
        }
        return res + need;
    }
}
```

#### [22. 括号生成](https://leetcode-cn.com/problems/generate-parentheses/)回溯思想
回溯法， 当右括号用的多 或者 左括号 or 右括号使用超支，当轮递归中止
否则 加入左括号和右括号做尝试
```java
class Solution {
    List<String> res = new ArrayList<>();

    public List<String> generateParenthesis(int n) {
        help("",n,n);
        return res;
    }

    public void help(String tem, int l, int r) {
        if (l > r || l < 0 || r < 0) return;
        if(l == 0 && r == 0) {
            res.add(tem);
            return;
        }
        help(tem+'(',l-1,r);
        help(tem+')',l,r-1);
    }
}
```
```python
class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        if n == 0 : return []
        tem,res = [],[]

        def recur(tem,left,right):

# 当右括号用的多 或者 左括号 or 右括号使用超支，当轮递归中止
            if left > right: return
            if left < 0 or right < 0 : return

            if left == 0 and right == 0:
                res.append(''.join(tem))
                return
                
            tem.append('(')
            recur(tem,left-1,right)
            tem.pop()
            
            tem.append(')')
            recur(tem,left,right-1)
            tem.pop()
            
        recur(tem,n,n)
        return res
```

#### [最长有效括号](https://leetcode-cn.com/problems/longest-valid-parentheses/)
- 动态规划，dp定义为以 s[i] 为结尾最长有效括号，所以当前为（，dp[i] = 0,顺便加入当前索引到栈内
- 若为 ），栈为空，0，不为空，栈顶出栈，且栈顶到i匹配，再加上栈顶前一个匹配到的最长括号即为当前最长结果
- 假如输入为“()()(())))()”,DP 为[0, 2, 0, 4, 0, 0, 2, 8, 0, 0, 0, 2]
```java
class Solution {
    public int longestValidParentheses(String s) {
        if (s == null || s.length() == 0) return 0;
        int[] dp = new int[s.length()];
        Stack<Integer> stack = new Stack<>();

        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == '(') {
                dp[i] = 0;
                stack.push(i);
            } else {
                if (!stack.isEmpty()) {
                    int index = stack.pop();
                    if(index != 0) dp[i] = dp[index - 1] + i - index + 1;
                    else dp[i] = i - index + 1;
                }else {
                    dp[i] = 0;
                }
            }
        }
        return Arrays.stream(dp).max().getAsInt();
    }
}
```
python代码
```python
class Solution:
    def longestValidParentheses(self, s: str) -> int:
        if not s: return 0
        dp = [0]*len(s)
        stack = []
        for i in range(len(s)):
            if s[i] == '(':
                dp[i] = 0
                stack.append(i) 
            if s[i] == ')':
                if stack:
                    index = stack.pop()
                    dp[i] = i - index +1 + dp[index-1]
                else: dp[i] = 0
        return max(dp)
```

#### [翻转单词顺序](https://leetcode-cn.com/problems/fan-zhuan-dan-ci-shun-xu-lcof/)

- 倒序遍历字符串 s ，记录单词左右索引边界 i , j ；

- 每确定一个单词的边界，则将其添加至单词列表 res ；
- 最终，将单词列表拼接为字符串，并返回即可

**python**

```python
class Solution:
    def reverseWords(self, s: str) -> str:
        s = s.strip() # 删除首尾空格
        i = j = len(s) - 1
        res = []
        while i >= 0:
            while i >= 0 and s[i] != ' ': i -= 1 # 搜索首个空格
            res.append(s[i + 1: j + 1]) # 添加单词
            while s[i] == ' ': i -= 1 # 跳过单词间空格
            j = i # j 指向下个单词的尾字符
        return ' '.join(res) # 拼接并返回
```

**java**

```java
class Solution {
    public String reverseWords(String s) {
        s = s.trim(); // 删除首尾空格
        int j = s.length() - 1, i = j;
        StringBuilder res = new StringBuilder();
        while(i >= 0) {
            while(i >= 0 && s.charAt(i) != ' ') i--; // 搜索首个空格
            res.append(s.substring(i + 1, j + 1) + " "); // 添加单词
            while(i >= 0 && s.charAt(i) == ' ') i--; // 跳过单词间空格
            j = i; // j 指向下个单词的尾字符
        }
        return res.toString().trim(); // 转化为字符串并返回
    }
}
```

#### 滑动窗口之[ 最长不含重复字符的子串（数组）](https://leetcode-cn.com/problems/zui-chang-bu-han-zhong-fu-zi-fu-de-zi-zi-fu-chuan-lcof/)

滑动窗口，右指针向右遍历的过程中看看当前元素是否见过，如果见过，那么见过元素及其之前肯定是用不了了，所以更新左指针为见过元素的下一个
。遍历的过程中，每次都加入元素和索引，计算最大子串长度是否超过记录值
```java
public class Solution {
    public int maxLength (int[] arr) {
        HashMap<Integer,Integer> map = new HashMap<>();
        int result = 0;
        for (int left = 0, right = 0; right < arr.length; right++) {
            if(map.containsKey(arr[right])) left = Math.max(left,map.get(arr[right])+1);
            result = Math.max(result, right - left +1);
            map.put(arr[right], right);
        }
        return result;
    }
}
```

子串：python解法（对比学习二者数据结构）

```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        hmap = dict()
        left,res = 0,0
        for i in range(len(s)):
            # 在遍历的过程中不停的维护左边界
            if s[i] in hmap:
                left = max(left,hmap[s[i]]+1)
            # 看当前没有重复数字的序列有没有超过记录
            res = max(res,i-left+1)
            hmap[s[i]] = i
        return res
```

#### 滑动窗口之[最小覆盖子串](https://leetcode-cn.com/problems/minimum-window-substring/) 

```python
class Solution:
    def minWindow(self, s: str, t: str) -> str:
        res = (0, float("inf"))
        t_counter = Counter(t)
        left = 0
        need = len(t)
        for right in range(len(s)):
            if s[right] in t_counter:
                if t_counter[s[right]] > 0:
                    need -= 1
                t_counter[s[right]] -= 1
                
                # when slide window includes every chars in t
                while not need:
                    # build up result
                    if right - left + 1 < res[1] - res[0] + 1:
                        res = (left, right)
                    # move left pointer
                    if s[left] in t_counter:
                        if t_counter[s[left]] == 0:
                            
                            need += 1
                        t_counter[s[left]] += 1
                    left += 1
                    
        return "" if res[1] == float("inf") else s[res[0]:res[1] + 1]
```

#### [最长递增子序列](https://leetcode-cn.com/problems/longest-increasing-subsequence/)

**解法一：动态规划**

dp[*i*] 的值代表 `nums` 前 i 的最长子序列长度

```python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        dp = [1]*len(nums)
        for i in range(1,len(nums)):
            for j in range(0,i):
                if nums[i] > nums[j]:
                    dp[i] = max(dp[i],dp[j]+1)
        return max(dp)
```

**解法二：二分法**

比如序列是78912345，前三个遍历完以后tail是789，这时候遍历到1，就得把1放到合适的位置，于是在tail二分查找1的位置，变成了189（如果序列在此时结束，因为res不变，所以依旧输出3），再遍历到2成为129，然后是123直到12345

```Python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        size = len(nums)
        if size<2:
            return size
        
        cell = [nums[0]]
        for num in nums[1:]:
            if num>cell[-1]:
                cell.append(num)
                continue
            
            l,r = 0,len(cell)-1
            while l<r:
                mid = l + (r - l) // 2
                if cell[mid]<num:
                    l = mid + 1
                else:
                    r = mid
            cell[l] = num
        return len(cell)

作者：coldme-2
链接：https://leetcode-cn.com/problems/longest-increasing-subsequence/solution/zui-chang-shang-sheng-zi-xu-lie-dong-tai-gui-hua-e/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```



#### [最长公共子序列](https://leetcode-cn.com/problems/longest-common-subsequence/)

```python
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        m,n = len(text1), len(text2)
        dp = [(n+1)*[0] for i in range(m+1)]
        for i in range(1,m+1):
            for j in range(1,n+1):
                if text1[i-1] == text2[j-1] :
                    dp[i][j] = dp[i-1][j-1]+1
                else:
                    dp[i][j] = max(dp[i-1][j],dp[i][j-1])
        return dp[m][n]
```

#### [最长公共子串](https://www.nowcoder.com/practice/f33f5adc55f444baa0e0ca87ad8a6aac?tpId=117&rp=1&ru=%2Fta%2Fjob-code-high&qru=%2Fta%2Fjob-code-high%2Fquestion-ranking)

```java
    public String LCS (String str1, String str2) {
        int m = str1.length(), n = str2.length();
        int[][] dp = new int[m + 1][n + 1];
        int max = 0, index = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (str1.charAt(i) == str2.charAt(j)) {
                    dp[i + 1][j + 1] = dp[i][j] + 1;
                    if (max < dp[i + 1][j + 1]) {
                        max = dp[i + 1][j + 1];
                        index = i + 1;
                    }
                }
            }
        }
        return max == 0 ? "-1" : str1.substring(index-max,index);
    }
}
```

#### [最长回文子串](https://www.nowcoder.com/practice/b4525d1d84934cf280439aeecc36f4af?tpId=117&tags=&title=&difficulty=0&judgeStatus=0&rp=0)

```python
class Solution:
    def getLongestPalindrome(self, A, n):
        # 求最长回文子串的方法,引入两个边界是针对abba,aba类似的这两类回文子串的判断
        def Palindrome(A,l,r):
            while l >= 0 and r<len(A) and A[l] == A[r]:
                l -= 1
                r += 1
            # 数组切片是左闭右开
            return A[l+1:r]
        res = 0
        for i in range(len(A)):
            l1 = Palindrome(A, i, i)
            l2 = Palindrome(A, i, i+1)
            res = max(res,len(l1),len(l2))
        return res
```

**如果要返回具体子串的low解法**

```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        def palindrome(s,l,r):
            while l>=0 and r<len(s) and s[l]==s[r]:
                l -= 1
                r += 1
            return r-l+1

        maxlen = 0
        res = ''
        for i in range(len(s)):
            l1 = palindrome(s,i,i)-2
            if l1>maxlen:
                maxlen = l1
                res = s[i-l1//2:i+l1//2+1]

            l2 = palindrome(s,i,i+1)-2
            if l2>maxlen:
                maxlen = l2
                res = s[i-l2//2+1:i+l2//2+1]
        return res
```

#### [回文子串的数量](https://leetcode-cn.com/problems/palindromic-substrings/)

```python
class Solution:
    def countSubstrings(self, s: str) -> int:
        def numPalindrome(s, l, r):
                num = 0
                while l>=0 and r<len(s) and s[l] == s[r]:
                    num += 1
                    l -= 1
                    r += 1
                return num
        res = 0
        for i in range(len(s)):
            res += numPalindrome(s,i,i)
            res += numPalindrome(s,i,i+1)
        return res
```

#### [最长公共前缀](https://leetcode-cn.com/problems/longest-common-prefix/)

- 当字符串数组长度为 0 时则公共前缀为空，直接返回
- 令最长公共前缀 ans 的值为第一个字符串，进行初始化
- 遍历后面的字符串，依次将其与 ans 进行比较，两两找出公共前缀，最终结果即为最长公共前缀
- 如果查找过程中出现了 ans 为空的情况，则公共前缀不存在直接返回
- 时间复杂度：O(s)，s 为所有字符串的长度之和

python

```python
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        if len(strs) == 0: # 当字符串数组长度为 0 时则公共前缀为空，直接返回
            return ""
        ans = strs[0] # 令最长公共前缀 ans 的值为第一个字符串，进行初始化
        for i in range(1, len(strs)): # 遍历后面的字符串，依次将其与 ans 进行比较，两两找出公共前缀，最终结果即为最长公共前缀
            idx = 0
            for cha1, cha2 in zip(ans, strs[i]):
                if cha1 != cha2:
                    break
                idx += 1
            ans = ans[0:idx]
            if ans == "": # 如果查找过程中出现了 ans 为空的情况，则公共前缀不存在直接返回
                return ans
        return ans
                
```

java代码

```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if(strs.length == 0) 
            return "";
        String ans = strs[0];
        for(int i =1;i<strs.length;i++) {
            int j=0;
            for(;j<ans.length() && j < strs[i].length();j++) {
                if(ans.charAt(j) != strs[i].charAt(j))
                    break;
            }
            ans = ans.substring(0, j);
            if(ans.equals(""))
                return ans;
        }
        return ans;
    }
}
```

#### [字符串转换成整数](https://leetcode-cn.com/problems/ba-zi-fu-chuan-zhuan-huan-cheng-zheng-shu-lcof/)

```python
class Solution:
    def myAtoi(self, s: str) -> int:
        res = 0; i =0 ; flag = 1
        s = s.lstrip()
        if not s: return 0
        if s[i] == '-': flag = 0
        if s[i] == '-' or s[i] == '+': i += 1
        while(i < len(s) and s[i].isdigit()):
            r = int(s[i]) - 0
            res = res*10 + r
            if (res >= 2147483648): return 2147483647 if flag else -2147483648
            i += 1
        return res if flag else -res
```

#### [字符串相乘](https://leetcode-cn.com/problems/multiply-strings/)

处理大数相乘，列竖式模拟，核心是：**num1[i] 和 num2[j] 的乘积对应的就是 res[i+j] 和 res[i+j+1] 这两个位置。**

```python
class Solution:
    def multiply(self, num1: str, num2: str) -> str:
        l1 = len(num1); l2 = len(num2)
        res = [0]*(l1+l2)
        for i in range(l1-1,-1,-1):
            for j in range(l2-1,-1,-1):
                mutil = res[i+j+1] + int(num1[i])*int(num2[j]) #不要忘了先把原来位置的值加上去
                res[i+j+1] = mutil%10
                res[i+j] += mutil//10
        for i,j in enumerate(res): # 去掉前置0 eg.([0, 4, 5, 7, 8, 8])
            if j != 0: return ''.join(map(str,res[i:]))
        return '0'
```

#### [394. 字符串解码](https://leetcode-cn.com/problems/decode-string/)
- 多加两个变量，count栈 和 res栈，分别代表下一轮递归要成多少次，当前递归内字符串是多少
- 遍历的过程中遇到数字和字母正常叠加处理即可
- 遇到左括号，count和res压入栈内，并且开启下一个轮次，count和res重新赋值
- 遇到右括号，清空当前轮次内容，res是轮内数据，mutil*res + 之前轮次内容等于上一个轮次的结果，不停的取出，就可以求解该问题
```java
class Solution {
    public String decodeString(String s) {
        String res = "";
        int mutil = 0;
        Stack<Integer> mutil_stack = new Stack<>();
        Stack<String> str_stack = new Stack<>();
        for (char c : s.toCharArray()) {
            if (c == '[') {
                mutil_stack.push(mutil);
                str_stack.push(res);
                mutil = 0;
                res = "";
            } else if (c == ']') {
                String tem = "";
//                得专门提取出来count，如果写在循环里面，会运行一次写一次导致空指针异常
                int count = mutil_stack.pop();
                for (int i = 0; i < count; i++) {
                    tem += res;
                }
                res = str_stack.pop() + tem;
            }else if(c>='0' && c<='9') mutil = mutil * 10 + Integer.parseInt(c + "");
            else res += c;
        }
        return res;
    }
}
```
python代码
```PYTHON
class Solution:
    def decodeString(self, s: str) -> str:
        stack, res, multi = [], "", 0
        for c in s:
            if c == '[':
                stack.append([multi, res])
                res, multi = "", 0
            elif c == ']':
                cur_multi, last_res = stack.pop()
                res = last_res + cur_multi * res
            elif '0' <= c <= '9':
                multi = multi * 10 + int(c)            
            else:
                res += c
        return res
```

递归解法，还需要好好再理解理解递归

```python
class Solution:
    def decodeString(self, s: str) -> str:
        def dfs(s, i):
            res, multi = "", 0
            while i < len(s):
                if '0' <= s[i] <= '9':
                    multi = multi * 10 + int(s[i])
                elif s[i] == '[':
                    i, tmp = dfs(s, i + 1)
                    res += multi * tmp
                    multi = 0
                elif s[i] == ']':
                    return i, res
                else:
                    res += s[i]
                i += 1
            return res
        return dfs(s,0)

作者：jyd
链接：https://leetcode-cn.com/problems/decode-string/solution/decode-string-fu-zhu-zhan-fa-di-gui-fa-by-jyd/
```

#### [比较版本号](https://leetcode-cn.com/problems/compare-version-numbers/)

转化成数组，在循环时用or连接，并为每一次比较赋初值0，然后比较可以保证每一位参与比较

```python
class Solution:
    def compareVersion(self, version1: str, version2: str) -> int:
        m = version1.split('.'); n = version2.split('.')
        lm = len(m); ln = len(n)
        i = 0; j = 0
        while i<lm or j < ln:
            a = 0; b = 0
            if i < lm: a = int(m[i])
            if j < ln: b = int(n[j])
            i += 1; j += 1
            if a != b: return -1 if a<b else 1
        return 0
```

## 动态规划

#### 青蛙跳台阶问题。

一只青蛙一次可以跳上1级台阶，也可以跳上2级台阶。求该青蛙跳上一个n级台阶总共有多少种跳法？

**分析：**

当n = 1， 只有1中跳法；当n = 2时，有2种跳法；当n = 3 时，有3种跳法；当n = 4时，有5种跳法；当n = 5时，有8种跳法；.......规律类似于Fibonacci数列：

![图片说明](https://uploadfiles.nowcoder.com/images/20191126/5459305_1574726608577_F3E7B4A76AD61143F52E38396E259B80)

所以，我们马上可以写出如下的递归实现代码：

```
public int Fibonacci(int n){  
    if(n<=2)  
        return n;  
    return Fibonacci(n-1)+Fibonacci(n-2);  
}  
```

当我们写出递归代码时，面试官应该会建议我们对递归代码进行优化，因为递归代码中有太多的重复运算。所以，我们考虑使用使用变量保存住中间结果。 代码实现如下：

```java
public int jumpFloor(int number) {  
    if(number<=2)  
        return number;  
    int jumpone=2; // 离所求的number的距离为1步的情况，有多少种跳法  
    int jumptwo=1; // 离所求的number的距离为2步的情况，有多少种跳法  
    int sum=0;  
    for(int i=3;i<=number;i++){  
        sum=jumptwo+jumpone;  
        jumptwo=jumpone;  
        jumpone=sum;  
    }  
    return sum;  
}
```

接下来，我们继续看青蛙跳台阶的变态版。

**题目二：青蛙变态跳台阶问题**

一只青蛙一次可以跳上1级台阶，也可以跳上2级……它也可以跳上n级。求该青蛙跳上一个n级的台阶总共有多少种跳法。

**思路：**

- 先跳到n-1级，再一步跳到n级，有f(n-1)种；
- 先跳到n-2级，再一步跳到n级，有f(n-2)种；
- 先跳到n-3级，再一步跳到n级，有f(n-3)种；
- ……
- 先跳到第1级，再一步跳到n级，有f(1)种；



所以，可以推出如下的公式：

- f(n)=f(n-1)+f(n-2)+f(n-3)+•••+f(1)
- f(n-1)=f(n-2)+f(n-3)+•••+f(1)
- 推出f(n)=2*f(n-1)

**算法实现如下：**

```java
public int jumpFloor2(int num) {  
    if(num<=2)  
        return num;  
    int jumpone=2; // 前面一级台阶的总跳法数  
    int sum=0;  
    for(int i=3;i<=num;i++){  
        sum = 2*jumpone;  
        jumpone = sum;  
    }  
    return sum;  
}
```

#### [不同路径](https://leetcode-cn.com/problems/unique-paths/)

```Python
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        dp = [[1]*n for i in range(m)]
        for i in range(1,m):
            for j in range(1,n):
                dp[i][j] = dp[i-1][j]+dp[i][j-1]
        return dp[m-1][n-1]
```

扩展：如果有障碍，则[dp[i][j]=0]()

#### **[编辑距离(二)](https://www.nowcoder.com/practice/05fed41805ae4394ab6607d0d745c8e4?tpId=117&&tqId=37801&rp=1&ru=/ta/job-code-high&qru=/ta/job-code-high/question-ranking)**

```python
class Solution:
    def minEditCost(self , word1: str, word2: str, ic: int, dc: int, rc: int) -> int:
        x = len(word1)+1; y = len(word2)+1
        dp = [[0]*y for i in range(x)]
        for j in range(1,y): dp[0][j] = dp[0][j-1] + ic
        for i in range(1,x): dp[i][0] = dp[i-1][0] + dc
        for i in range(1,x):
            for j in range(1,y):
                # 因为添加了首行首列 所以判断实际 i j 比word的索引快了一步
                if word1[i-1] == word2[j-1]: dp[i][j] = dp[i-1][j-1]
                # 三种操作依次为删除 添加 替换
                else:dp[i][j] = min(dp[i-1][j]+dc,dp[i][j-1]+ic,dp[i-1][j-1]+rc)
        return dp[-1][-1]
```

#### [最大正方形](https://leetcode-cn.com/problems/maximal-square/)

当我们判断以某个点为正方形右下角时最大的正方形时，那它的上方，左方和左上方三个点也一定是某个正方形的右下角，否则该点为右下角的正方形最大就是它自己了。这是定性的判断，那具体的最大正方形边长呢？我们知道，该点为右下角的正方形的最大边长，最多比它的上方，左方和左上方为右下角的正方形的边长多1，最好的情况是是它的上方，左方和左上方为右下角的正方形的大小都一样的，这样加上该点就可以构成一个更大的正方形。 但如果它的上方，左方和左上方为右下角的正方形的大小不一样，合起来就会缺了某个角落，这时候只能取那三个正方形中最小的正方形的边长加1了。**假设dpi表示以i,j为右下角的正方形的最大边长，则有 dp[i][j] = min(dp[i-1][j-1], dp[i-1][j], dp[i][j-1]) + 1** 当然，如果这个点在原矩阵中本身就是0的话，那dp[i]肯定就是0了。

```python
class Solution:
    def maximalSquare(self, matrix: List[List[str]]) -> int:
        m = len(matrix); n = len(matrix[0]); res = 0
        dp = [[0]*(n+1) for i in range(m+1)]
        for i in range(m):
            for j in range(n):
                if matrix[i][j] == '1':
                    dp[i+1][j+1] = min(dp[i][j+1],dp[i+1][j],dp[i][j])+1
                    res = max(res,dp[i+1][j+1])
        return res*res
```

#### [53. 最大子序和](https://leetcode-cn.com/problems/maximum-subarray/)

我的low 解法：前缀和，**前缀和之差就等于子串和**

```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        if len(nums) == 1: return nums[0]
        prefix = [nums[0]]
        res = nums[0]
        min1 = nums[0]
        for i in range(1,len(nums)):
            prefix.append(prefix[-1]+nums[i])
            min1 = min(min1,prefix[i-1])
            res = max(res,prefix[i]-min1)
        return max(res,max(prefix))
```

当前位置结尾的最大序列长度，**要么前一个加当前，要么自成体系**

![image-20220405170059060](images/image-20220405170059060.png)

```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        dp = [0]*len(nums)
        dp[0] = nums[0]
        for i in range(1,len(nums)):
            dp[i] = max(nums[i],dp[i-1]+nums[i])
        return max(dp)
```

三行代码

```python
for i in range(1, len(nums)):
      nums[i]= nums[i] + max(nums[i-1], 0)
        return max(nums)
```

#### [乘积最大子数组](https://leetcode-cn.com/problems/maximum-product-subarray/)

```python
class Solution:
    def maxProduct(self, nums: List[int]) -> int:
        l = len(nums)
        dp = [[nums[0]] * 2 for i in range(l)]

        for i in range(1, l):
            if nums[i] > 0:
                dp[i][1] = max(nums[i], nums[i] * dp[i - 1][1])
                dp[i][0] = min(nums[i], nums[i] * dp[i - 1][0])
            else:
                dp[i][1] = max(nums[i], nums[i] * dp[i - 1][0])
                dp[i][0] = min(nums[i], nums[i] * dp[i - 1][1])

        res = dp[0][1]
        for i in range(l):
            res = max(res, dp[i][1])

        return res
```



#### [正则表达式匹配](https://leetcode-cn.com/problems/regular-expression-matching/)

4.5该解法还不太懂

1. 先判断s和p的第一个字符是否匹配
2. 处理p[1]为`*`号的情况：匹配0个或多个字符
3. 处理`.`号的情况：匹配一个字符

```python
class Solution:
    def isMatch(self, s: str, p: str) -> bool:
        if not p: return not s  # 结束条件

        first_match = (len(s) > 0) and p[0] in {s[0], '.'}
        # 先处理 `*`
        if len(p) >=2 and p[1] == '*':
            # 匹配0个 | 多个
            return self.isMatch(s, p[2:]) or (first_match and self.isMatch(s[1:], p))
        
        # 处理 `.` ，匹配一个
        return first_match and self.isMatch(s[1:], p[1:])

```



#### [买卖股票的最佳时机](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/)

最初版本：遍历时记录下最低成本，如果新的卖出价获益更高则更新，否则保持记录

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        if len(prices) == 0: return 0
        dp = [0]*len(prices)
        cost = prices[0]
        for i in range (1,len(prices)):
            cost = min(cost,prices[i])
            dp[i] = max(dp[i-1],prices[i]-cost) 
        return max(dp)
```

优化空间复杂度：利润只与前一天利润和当前成本有关，所以利润只保留最大值

```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        if len(prices) == 0: return 0
        profit = 0
        cost = prices[0]
        for i in range (1,len(prices)):
            cost = min(cost,prices[i])
            profit = max(profit,prices[i]-cost) 
        return profit
```

重新定义dp数组定义，`便于后续扩展  dp[i][0]表示某一天不持股到该天为止的最大收益，dp[i][1]表示某天持股，到该天为止的最大收益 fast-template`

```java
import java.util.*;
public class Solution {
    public int maxProfit (int[] prices) {
        int n = prices.length;
        int[][] dp = new int[n][2];
        dp[0][0] = 0;
        dp[0][1] = -prices[0];
        for (int i = 1; i < n; i++) {
            dp[i][0] = Math.max(dp[i - 1][0], dp[i - 1][1] + prices[i]);
            dp[i][1] = Math.max(dp[i - 1][1], -prices[i]);
        }
        return dp[n - 1][0];
}
```

#### [买卖股票的最佳时机 II](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/)

可以多次买卖，因此如果第i天持有，有可能是前一天不持有，当天买入，收益为前一天不持有的收益-当天买入价格

```java
class Solution {
    public int maxProfit(int[] prices) {
        int n = prices.length;
        int[][] dp = new int[n][2];
        dp[0][0] = 0;
        dp[0][1] = -prices[0];
        for (int i = 1; i < n; i++) {
            dp[i][0] = Math.max(dp[i - 1][0], dp[i - 1][1] + prices[i]);
            // 与前一题的区别只在这里
            dp[i][1] = Math.max(dp[i - 1][1], dp[i - 1][0]-prices[i]);
        }
        return dp[n - 1][0];
    }
}
```

#### [买卖股票的最佳时机 III](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-iii/)

最多完成两笔交易

![image-20220405220322248](http://pic.wyydd.top/image-20220405220322248.png)

```java
import java.util.*;
public class Solution {
    public int maxProfit (int[] prices) {
        int n = prices.length;
        int[][] dp = new int[n][5];
        //初始化dp为最小 fast-template
        Arrays.fill(dp[0], -10000);
        //第0天不持有状态
        dp[0][0] = 0;
        //第0天持有股票
        dp[0][1] = -prices[0];
        //状态转移
        for (int i = 1; i < n; i++) {
            dp[i][0] = dp[i - 1][0];
            dp[i][1] = Math.max(dp[i - 1][1], dp[i - 1][0] - prices[i]);
            dp[i][2] = Math.max(dp[i - 1][2], dp[i - 1][1] + prices[i]);
            dp[i][3] = Math.max(dp[i - 1][3], dp[i - 1][2] - prices[i]);
            dp[i][4] = Math.max(dp[i - 1][4], dp[i - 1][3] + prices[i]);
        }
        //选取最大值，可以只操作一次
        return Math.max(dp[n - 1][2], Math.max(0, dp[n - 1][4]));}
}
```

#### [打家劫舍1](https://leetcode-cn.com/problems/house-robber/)

`dp[i] = Math.max(dp[i-1],nums[i-1]+dp[i-2]);`

python解法

```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        dp = [0]*(len(nums)+1)
        dp[1] = nums[0]
        for i in range(2,len(nums)+1):
            dp[i] = max(dp[i-1],nums[i-1]+dp[i-2])
        return dp[-1]
```

java

```java
class Solution {
    public int rob(int[] nums) {
        int[] dp = new int[nums.length+1];
        dp[1] = nums[0];
        for(int i = 2; i<=nums.length; i++){
            dp[i] = Math.max(dp[i-1],nums[i-1]+dp[i-2]);
        }
        return dp[nums.length];
    }
}
```

#### [打家劫舍 II](https://leetcode-cn.com/problems/house-robber-ii/)

围成一个环，核心在于 **第一个和最后一个只能选一个。**

- 如果选第一个，那么返回dp[-2];
- 如果选第一个，那么dp[1] = 0; 返回dp[-1]
- 最终返回二者最大值即可 （特殊情况：当只有一个数的时候返回他即可）

python

```python
class Solution:
    def rob(self, nums: List[int]) -> int:
        l = len(nums)
        if l == 1: return nums[0]
        dp = [0 for i in range(l+1)]
        dp[1] = nums[0]
        for i in range(2,len(nums)+1):
            dp[i] = max(dp[i-1],nums[i-1]+dp[i-2])
        res = dp[-2]
        dp[1] = 0 
        for i in range(2,len(nums)+1):
            dp[i] = max(dp[i-1],nums[i-1]+dp[i-2])
        return max(res,dp[-1])
```

java

```java
class Solution {
    public int rob(int[] nums) {
        int l = nums.length;
        if(l == 1) return nums[0];
        int[] dp = new int[l+1];
        dp[1] = nums[0];
        for(int i = 2; i<= l; i++){
            dp[i] = Math.max(dp[i-1],dp[i-2]+nums[i-1]);
        }
        int res = dp[l-1];
        dp[1] = 0; 
        for(int i = 2; i<=l; i++){
            dp[i] = Math.max(dp[i-1],nums[i-1]+dp[i-2]);
        }
        return Math.max(res,dp[l]);
    }
}
```

#### [背包问题](https://leetcode-cn.com/problems/coin-change/solution/yi-tao-kuang-jia-jie-jue-bei-bao-wen-ti-h0y40/)

背包问题是一类经典的动态规划问题，它非常灵活，需要仔细琢磨体会，本文先对背包问题的几种常见类型作一个总结，期望可以用一套框架解决背包问题。
常见背包问题可分为：

**01 背包问题：**
最基本的背包问题就是 01 背包问题：一共有 N 件物品，第 i（i 从 1 开始）件物品的重量为 w[i]，价值为 v[i]。在总重量不超过背包承载上限 W 的情况下，能够装入背包的最大价值是多少？

**完全背包问题：**
完全背包与 01 背包不同就是每种物品可以有无限多个：一共有 N 种物品，每种物品有无限多个，第 i（i 从 1 开始）种物品的重量为 w[i]，价值为 v[i]。在总重量不超过背包承载上限 W 的情况下，能够装入背包的最大价值是多少？
可见 01 背包问题与完全背包问题主要区别就是物品是否可以重复选取。

背包问题具备的特征：
是否可以根据一个 target（直接给出或间接求出），target 可以是数字也可以是字符串，再给定一个数组 arrs，问：能否使用 arrs 中的元素做各种排列组合得到 target。

**背包问题解法：**
**01 背包问题：**
**如果是 01 背包，即数组中的元素不可重复使用，外循环遍历 arrs，内循环遍历 target，且内循环倒序:**

**完全背包问题：**
**（1）如果是完全背包，即数组中的元素可重复使用并且不考虑元素之间顺序，arrs 放在外循环（保证 arrs 按顺序），target在内循环。且内循环正序。**
**（2）如果组合问题需考虑元素之间的顺序，需将 target 放在外循环，将 arrs 放在内循环，且内循环正序。**

作者：wulafly-2
链接：https://leetcode-cn.com/problems/partition-equal-subset-sum/solution/yi-tao-kuang-jia-jie-jue-bei-bao-wen-ti-p9saf/

https://leetcode-cn.com/problems/coin-change/solution/yi-pian-wen-zhang-chi-tou-bei-bao-wen-ti-sq9n/

##### 01背包问题

###### [分割等和子集](https://leetcode-cn.com/problems/partition-equal-subset-sum/)

```python
class Solution:
    def canPartition(self, nums: List[int]) -> bool:
        s = sum(nums)
        if s&1 == 1: return False
        else: target = s >> 1
        dp = [False]*(target+1)
        dp[0] = True
        for num in nums:
            for i in range(target,num-1,-1):
                dp[i] = dp[i] or dp[i-num]
        return dp[target]
```

###### [目标和](https://leetcode-cn.com/problems/target-sum/)

**`nums` 中存在几个子集 `A`，使得 `A` 中元素的和为 `(target + sum(nums)) / 2`**？

```python
class Solution:
    def findTargetSumWays(self, nums: List[int], target: int) -> int:
        s = sum(nums)
        if target>s or (s+target)&1 == 1: return 0
        else: target = (s+target)//2
        dp = [0]*(abs(target)+1)
        dp[0] = 1
        for num in nums:
            for i in range(target,num-1,-1):
                dp[i] = dp[i] + dp[i-num]
        return dp[target]
```

##### 完全背包



#### 高楼仍鸡蛋



## 回溯算法 子集、组合、分割

回溯算法框架：

```python
result = []
def backtrack(路径, 选择列表):
    if 满足结束条件:
        result.add(路径)
        return
    
    for 选择 in 选择列表:
        做选择
        backtrack(路径, 选择列表)
        撤销选择
```

**有些朋友可能会疑惑什么时候使用 used 数组，什么时候使用 begin 变量。这里为大家简单总结一下：**

- **排列问题，讲究顺序（即 [2, 2, 3] 与 [2, 3, 2] 视为不同列表时），需要记录哪些数字已经使用过，此时用 used 数组；**
- **组合问题，不讲究顺序（即 [2, 2, 3] 与 [2, 3, 2] 视为相同列表时），需要按照某种顺序搜索，此时使用 begin 变量。**

```java
import java.util.ArrayDeque;
import java.util.ArrayList;
import java.util.Deque;
import java.util.List;


public class Solution {

    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        int len = candidates.length;
        List<List<Integer>> res = new ArrayList<>();
        if (len == 0) {
            return res;
        }

        Deque<Integer> path = new ArrayDeque<>();
        dfs(candidates, 0, len, target, path, res);
        return res;
    }

    private void dfs(int[] candidates, int begin, int len, int target, Deque<Integer> path, List<List<Integer>> res) {
        if (target < 0) {
            return;
        }
        if (target == 0) {
            res.add(new ArrayList<>(path));
            return;
        }

        for (int i = begin; i < len; i++) {
            path.addLast(candidates[i]);
            System.out.println("递归之前 => " + path + "，剩余 = " + (target - candidates[i]));

            dfs(candidates, i, len, target - candidates[i], path, res);

            path.removeLast();
            System.out.println("递归之后 => " + path);

        }
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        int[] candidates = new int[]{2, 3, 6, 7};
        int target = 7;
        List<List<Integer>> res = solution.combinationSum(candidates, target);
        System.out.println("输出 => " + res);
    }
}

作者：liweiwei1419
链接：https://leetcode-cn.com/problems/combination-sum/solution/hui-su-suan-fa-jian-zhi-python-dai-ma-java-dai-m-2/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```



#### [排列](https://leetcode-cn.com/problems/permutations/)

做选择时如果新加入的数已经在选择列表里面了则返回

![image.png](https://pic.leetcode-cn.com/0bf18f9b86a2542d1f6aa8db6cc45475fce5aa329a07ca02a9357c2ead81eec1-image.png)

```python
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        path,res = [],[]
        def recur(nums,path):
            if len(path) == len(nums):
                res.append(list(path))
            for i in nums:
                if i in path:continue
                path.append(i)
                recur(nums,path)
                path.pop()
        recur(nums,path)
        return res
```

#### [排列（字符可重复）](https://leetcode-cn.com/problems/zi-fu-chuan-de-pai-lie-lcof/)

```python
class Solution:
    def permuteUnique(self, nums: List[int]) -> List[List[int]]:
        # 先排序才能用后面的判断
        nums.sort()
        path,res = [],[]
        def recur(nums,path,used):
            if len(path) == len(nums):
                res.append(path[:])
            for i in range(size):
                if not used[i]:
                    # 这一步的判断着实很关键
                    if i>0 and nums[i] == nums[i-1] and  used[i-1]:continue
                    used[i] = True
                    path.append(nums[i])
                    recur(nums,path,used)
                    used[i] = False
                    path.pop()
        size = len(nums)
        used = [False]*size
        recur(nums,path,used)
        return res
```

#### [组合](https://leetcode-cn.com/problems/combinations/)

**核心**：用`i`去控制选择范围![image.png](https://pic.leetcode-cn.com/1599488203-TzmCXb-image.png)

```python
class Solution:
    def combine(self, n: int, k: int) -> List[List[int]]:
        res = []
        path = [] 
        def recur(n,path,start):
            if len(path) == k:
                # 这里应该用深拷贝，如果只写path，path会随着后面的引用而改变
                res.append(path[:])
            for j in range(start,n+1):
                path.append(j)
                # 递归开始点为j+1而不是start+1
                recur(n,path,j+1)
                path.pop()
        recur(n,path,1)
        return res 
```

#### [ 子集](https://leetcode-cn.com/problems/subsets/)

![子集问题递归树.png](https://pic.leetcode-cn.com/d8e07f0c876d9175df9f679fcb92505d20a81f09b1cb559afc59a20044cc3e8c-%E5%AD%90%E9%9B%86%E9%97%AE%E9%A2%98%E9%80%92%E5%BD%92%E6%A0%91.png)

```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        res = []; path = []
        def recur(nums,start,path):
            res.append(path[:])
            for i in range(start,len(nums)):
                path.append(nums[i])
                print(path)
                recur(nums,i+1,path)
                path.pop()
        recur(nums,0,path)
        return res
```

![在这里插入图片描述](https://pic.leetcode-cn.com/7dd0461942d17bc38860b05a2b6a6461feae54ad141c64bfaace9127e1a29651.png)

#### [子集 II字符可重复](https://leetcode-cn.com/problems/subsets-ii/)

```python
class Solution:
    def subsetsWithDup(self, nums: List[int]) -> List[List[int]]:
        res = []; path = []
        def recur(nums,start,path):
            res.append(path[:])
            for i in range(start,len(nums)):
                if i>start and nums[i]==nums[i-1]:continue
                path.append(nums[i])
                recur(nums,i+1,path)
                path.pop()
        nums.sort()
        recur(nums,0,path)
        return res
```

![在这里插入图片描述](https://pic.leetcode-cn.com/95513b4b31c8570d7c3b4b29cb09169e1ae981800602ec44ff3cfa20d662b72a.png)

#### [组合总和](https://leetcode-cn.com/problems/combination-sum/)

```python
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        res = []; path = []
        l = len(candidates)
        def recur(nums,start,path,target,add):
            if add == target: res.append(path[:])
            for i in range(start,l):
                if add > target: continue
                path.append(nums[i])
                # i不用加一，因为可以重复利用
                recur(nums,i,path,target,add+candidates[i])
                path.pop()
        recur(candidates,0,path,target,0)
        return res
```

或者直接就是一个朴素做法

```python
class Solution:
    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        res = []; path = []
        def recur(candidates,target,path):
            if target <= 0:
                if target == 0:
                    tem = sorted(path)
                    if tem not in res:res.append(tem)
                else: return
            for num in candidates:
                path.append(num)
                recur(candidates,target-num,path)
                path.pop()
        recur(candidates,target,path)
        return res
```

#### [电话号码的字母组合](https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number/)

```python
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        if len(digits) == 0:return []
        result,tem = [],[]
        digital = [
            ' ',' ','abc','def','ghi','jkl','mno','pqrs','tuv','wxyz'
        ]
        def recur(digits,result,tem,index):
            if len(tem) == len(digits):
                result.append(''.join(tem))
                return
			# 遍历第一层 后面交给递归
            for j in digital[int(digits[index])]:
                tem.append(j)
                recur(digits,result,tem,index+1)
                tem.pop()

        recur(digits,result,tem,0)
        return result
```

#### [复原 IP 地址](https://leetcode-cn.com/problems/restore-ip-addresses/)

```python
class Solution:
    def restoreIpAddresses(self, s: str) -> List[str]:
        res,tem = [],[]
        def recur(s,index):
            if len(tem) == 4 or index == len(s):
                # 这里才是符合条件的
                if len(tem) == 4 and index == len(s):
                    res.append('.'.join(tem))
                # 这里是剪枝，比如 2.5.6.5.3.5和 3.2.6 就可以提前中止
                return
            for i in range(1,4):
                t = s[index:index+i]
                # t不为空的判断很重要，我之前就是每次在这里出错，比如 1.1.11在回退是t就为空了
                # 最后一个判断的意思是 t不能以0开头，但可以是0
                # 小于 255 必须转化为数字比较，不能直接比较字符串，这里我还不清楚为什么
                if t != '' and int(t) <= 255 and (t == '0' or t[0] != '0'):
                    tem.append(t)
                    recur(s,index+i)
                    tem.pop()
        recur(s,0)
        return res
```

#### [括号生成](https://leetcode-cn.com/problems/generate-parentheses/)

```python
class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        res, tem = [], []
        def recur(tem,l,r):
            # 当右括号用的多 或者 左括号 or 右括号使用超支，当轮递归中止
            if r > l: return
            if r>n or l>n: return
            if r == n and l == n: res.append(''.join(tem))
            
            tem.append('(')
            recur(tem,l+1,r)
            tem.pop()

            tem.append(')')
            recur(tem,l,r+1)
            tem.pop()
        recur(tem,0,0)
        return res
```

#### [N 皇后](https://leetcode-cn.com/problems/n-queens/)

```python
class Solution:
    def solveNQueens(self, n: int) -> List[List[str]]:
        def DFS(queens, xy_dif, xy_sum):
            p = len(queens)
            if p==n:
                result.append(queens)
                return 
            for q in range(n): 
                if q not in queens and p-q not in xy_dif and p+q not in xy_sum: 
                    DFS(queens+[q], xy_dif+[p-q], xy_sum+[p+q])  
        result = []
        DFS([],[],[])
        return [ ["."*i + "Q" + "."*(n-i-1) for i in sol] for sol in result]
```

```python
class Solution:
    def solveNQueens(self, n: int) -> List[List[str]]:
        res = []; tem = [['.']*n for _ in range(n)]

        def is_valid(tem,i,j):
            for m in range(i):
                if tem[m][j] == 'Q': return False
            for m in range(1,min(i,j)):
                if tem[i-m][j-m] == 'Q': return False
            for m in range(1,min(i,n-j-1)):
                if tem[i-m][j+m] == "Q": return False
            return True
            
        def recur(tem,row):
            if row == n:
                res.append(tem[:][:])
                return

            for col in range(n):
                if is_valid(tem,row,col): 
                    tem[row][col] = 'Q'
                    recur(tem,row+1)
                    tem[row][col] = '.'

        recur(tem,0)
        return tem
```

#### [划分为k个相等的子集](https://leetcode-cn.com/problems/partition-to-k-equal-sum-subsets/)

```python
class Solution:
    def canPartitionKSubsets(self, nums: List[int], k: int) -> bool:
        n=len(nums)
        tsum=sum(nums)
        if tsum%k!=0:return False
        target=tsum/k
        # 排序剪枝
        nums.sort(reverse=True)
        if nums[0]>target:return False
        used=[False] * n # 把数组分为两部分：已经满足target的group元素和待处理的剩下元素
        def dfs(cur,begin,k):
            if k==0:return True
            if cur>target:return False
            if cur==target: return dfs(0,0,k-1) # 剩下的元素是否能被等和分割成k-1份
            for i in range(begin,n):
                if not used[i]:
                    used[i]=True
                    if dfs(cur+nums[i],i+1,k): # 加上当前元素后能否被等和分割成k份
                        return True
                    used[i]=False # 可以帮助下一组（k-1）与这一组的元素区分开来
            return False
        return dfs(0,0,k)       
```

## 贪心和其他数学题

#### [56. 合并区间](https://leetcode-cn.com/problems/merge-intervals/)

```python
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        if not intervals:return []
        intervals.sort(key=lambda x: x[0])
        res = [intervals[0]]
        for x,y in intervals[1:]:
            if res[-1][1] < x: res.append([x,y])
            else: res[-1][1] = max(res[-1][1],y)
        return res
```

#### [分发糖果](https://www.nowcoder.com/practice/76039109dd0b47e994c08d8319faa352?tpId=295&tags=&title=&difficulty=0&judgeStatus=0&rp=0&sourceUrl=)

![image-20220406105447245](images/image-20220406105447245.png)

java

```java
import java.util.*;
public class Solution {
    public int candy (int[] arr) {
        int n = arr.length;
        if (n <= 1) return n;
        int[] nums = new int[n];
        Arrays.fill(nums,1);
        for (int i = 1; i < n; i++) {
            if(arr[i] > arr[i-1]) nums[i] = nums[i-1]+1;
        }
        int res = nums[n-1];
        for (int i = n - 2; i >= 0; i--) {
            if(arr[i]>arr[i+1] && nums[i] <= nums[i+1]) nums[i] = nums[i+1]+1;
            res += nums[i];
        }
        return res;
    }
}
```

#### [**主持人调度（二）**](https://www.nowcoder.com/practice/4edf6e6d01554870a12f218c94e8a299?tpId=295&sfm=html&channel=nowcoder)

python

```python
class Solution:
    def minmumNumberOfHost(self , n: int, startEnd: List[List[int]]) -> int:
        start = []; end = []
        for i in range(n):
            start.append(startEnd[i][0])
            end.append(startEnd[i][1])
        start.sort(); end.sort()
        res = 1; j = 0
        for i in range(1,n):
            if start[i] >= end[j]: j += 1
            else: res += 1
        return res
```

java

```java
import java.util.*;
public class Solution {
    public int minmumNumberOfHost (int n, int[][] startEnd) {
        int[] start = new int[n];
        int[] end = new int[n];
        for(int i= 0; i<n; i++){
            start[i] = startEnd[i][0];
            end[i] = startEnd[i][1];
        }
        Arrays.sort(start);
        Arrays.sort(end);
        int res = 1, j = 0;
        for (int i = 1; i < n; i++) {
            if(start[i] >= end[j]) j++;
            else res++;
        }
        return res; 
    }
}
```

#### [圆圈中最后剩下的数字](https://leetcode-cn.com/problems/yuan-quan-zhong-zui-hou-sheng-xia-de-shu-zi-lcof/)

这道题不算贪心，但是这种有意思的题也不好安排，故放置于此

![image.png](https://pic.leetcode-cn.com/9dda886441be8d249abb76e35f53f29fd6e780718d4aca2ee3c78f947fb76e75-image.png)

然后我们从最后剩下的 3 倒着看，我们可以反向推出这个数字在之前每个轮次的位置。

最后剩下的 3 的下标是 0。

第四轮反推，补上 mm 个位置，然后模上当时的数组大小 22，位置是(0 + 3) % 2 = 1。

第三轮反推，补上 mm 个位置，然后模上当时的数组大小 33，位置是(1 + 3) % 3 = 1。

第二轮反推，补上 mm 个位置，然后模上当时的数组大小 44，位置是(1 + 3) % 4 = 0。

第一轮反推，补上 mm 个位置，然后模上当时的数组大小 55，位置是(0 + 3) % 5 = 3。

所以最终剩下的数字的下标就是3。因为数组是从0开始的，所以最终的答案就是3。

总结一下反推的过程，就是 (当前index + m) % 上一轮剩余数字的个数。

```python
class Solution:
    def lastRemaining(self, n: int, m: int) -> int:
        x = 0
        for i in range(2, n + 1):
            x = (x + m) % i
        return x
```

#### [1823. 找出游戏的获胜者](https://leetcode-cn.com/problems/find-the-winner-of-the-circular-game/)

```python
class Solution:
    def findTheWinner(self, n: int, k: int) -> int:
        circle = [i for i in range(1,n+1)]
        index = 0
        for i in range(1,n):
            index = (index+k-1)%len(circle)
            circle.pop(index)
        return circle[0]
```



#### [ x 的平方根 ](https://leetcode-cn.com/problems/sqrtx/)

**解法一：二分法**

```python
class Solution:
    def mySqrt(self, x: int) -> int:
        l = 0
        r = x
        while l <= r:
            mid = (l+r)//2
            temp = mid**2
            if  temp < x:
                l = mid + 1
            elif temp > x:
                r = mid - 1
            elif temp == x:
                return mid
        # r一定会停在mid**2 <= x的最大那个mid的位置，因为mid**2=x的mid如果存在的话在上面
        # 就已经返回了，所以这里只需要返回r就好了
        return r 
```

**这道题一定要注意 保留到小数点后几位的变形体**

**解法二：牛顿迭代法**

![image-20220322103304432](http://pic.wyydd.top/image-20220322103304432.png)

```python
class Solution:
    def mySqrt(self, x: int) -> int:
        if x == 0: return 0
        x0 = float(x)
        while 1:
            x1 = (x0 + x/x0)*0.5
            if abs(x1-x0)<1e-3:
                return '%.3f'%x1
            x0 = x1
```

#### [扑克牌中的顺子](https://leetcode-cn.com/problems/bu-ke-pai-zhong-de-shun-zi-lcof/)

```python
class Solution:
    def isStraight(self, nums: List[int]) -> bool:
        joker = 0
        nums.sort() # 数组排序
        for i in range(4):
            if nums[i] == 0: joker += 1 # 统计大小王数量
            elif nums[i] == nums[i + 1]: return False # 若有重复，提前返回 false
        return nums[4] - nums[joker] < 5 # 最大牌 - 最小牌 < 5 则可构成顺子
```

[n个骰子的点数](https://leetcode-cn.com/problems/nge-tou-zi-de-dian-shu-lcof/)



## 位运算

```java
x & 1 == 1 or == 0 判断奇偶
x = x&（x-1) 清零最低位的1
x & -x   得到最低位的1
x ^ x = 0
```



#### 不用额外变量交换两个数

```java
a = a^b;
b = a^b;
a = a^b;
```

#### [剑指 Offer 65. 不用加减乘除做加法](https://leetcode-cn.com/problems/bu-yong-jia-jian-cheng-chu-zuo-jia-fa-lcof/)

```python
class Solution:
    def add(self, a: int, b: int) -> int:
        x = 0xffffffff
        a, b = a & x, b & x
        while b != 0:
            a, b = (a ^ b), (a & b) << 1 & x
        return a if a <= 0x7fffffff else ~(a ^ x)
```

#### 数组中出现了奇数次的数

x^x = 0; 0^x  = x;

```python
def singleNumber(self, nums: List[int]) -> List[int]:
    x = 0
    for num in nums:  # 1. 遍历 nums 执行异或运算
        x ^= num      
    return x;         # 2. 返回出现一次的数字 x
```

#### 数组中有两个数出现了奇数次

- 第一轮整体遍历，求出a^b（因为相同的数字异或为0，0异或任何数字为数字自身）
- 然后结合a^b以及原来数组求出这两个数字
  - 原理：用一个只有一位为1的数字来遍历异或整个数组，把这个数组分成两个子数组（异或结果相同的数字在同一个子数组），如果是两个相同的数字，它们一定在同一个子数组里（保证子数组异或时为0），现在只需要把两个只出现一次的数字分到不同的子数组，那么子数组分别遍历异或得到的两个数字就是这两个数字。
  - 怎么把两个只出现一次的数字分到不同地子数组？
    - 找到a^b第一个为1的位置，异或结果为1说明a和b在这一位上不同，那用只有这一位为1的数字m去分别异或a和b，得到的结果一定不同，也就把a和b分到了不同的子数组。结合上一点得出结果。

```python
class Solution:
    def singleNumbers(self, nums: List[int]) -> List[int]:
        x, y, n, m = 0, 0, 0, 1
        for num in nums:         # 1. 遍历异或
            n ^= num
        while n & m == 0:        # 2. 循环左移，计算 m
            m <<= 1       
        for num in nums:         # 3. 遍历 nums 分组
            if num & m: x ^= num # 4. 当 num & m != 0
            else: y ^= num       # 4. 当 num & m == 0
        return x, y              # 5. 返回出现一次的数字
```

#### [一个数出现一次，其余数出现三次](https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-ii-lcof/)

如果一个数字出现三次,那么它的二进制表示的每一位(0或者1)也出现三次。如果把所有出现三次的数字的二进制表示的每一位都分别加起来,那么每一位的和都能被3整除。如果某一位的和能被3整除,那么那个只出现一次的数字二进制表示中对应的那一位是0;否则就是1;

```java
public class Solution56_2 {
	
    public int singleNumber(int[] nums) {//本算法同样适用于数组nums中存在负数的情况
        if(nums.length==0) return -1;//输入数组长度不符合要求，返回-1;
        int[] bitSum = new int[32];//java int类型有32位，其中首位为符号位
        int res=0;
        for(int num:nums){
            int bitMask=1;//需要在这里初始化，不能和res一起初始化
            for(int i=31;i>=0;i--){//bitSum[0]为符号位
            	//这里同样可以通过num的无符号右移>>>来实现，否则带符号右移(>>)左侧会补符号位，对于负数会出错。
            	//但是不推荐这样做，最好不要修改原数组nums的数据
                if((num&bitMask)!=0) bitSum[i]++;//这里判断条件也可以写为(num&bitMask)==bitMask,而不是==1
                bitMask=bitMask<<1;//左移没有无符号、带符号的区别，都是在右侧补0
            }
        }
        for(int i=0;i<32;i++){//这种做法使得本算法同样适用于负数的情况
            res=res<<1;
            res+=bitSum[i]%3;//这两步顺序不能变，否则最后一步会多左移一次
        }
        return res;
    }
}
```

## java手撕高频题

#### 单例模式

```java
public class Single {
    public static void main(String[] args) {

    }
}

/**
 *饿汉式的单例模式
 * @author ywq
 */
class Single1{
    private Single1(){}
    private static final Single s = new Single();
    public static Single getInstance(){
        return s;
    }
}

/**
 *懒汉式的单例模式
 * @author ywq
 */
class Single2{
    private Single2(){}
    private static Single s = null;
    public static  Single getInstance(){
        if(null==s)
            s = new Single();
        return s;
    }
}

/**
 * 多线程环境下的懒汉式单例模式(DCL，双检锁实现)
 * @author ywq
 */
class Single3{
    private static Single s = null;
    private Single3(){}

    public static  Single getInstance(){
        if(null==s){
            synchronized(Single.class){
                if(null==s)
                /**
                 * 1. 分配内存空间
                 * 2. 执行构造方法，初始化对象
                 * 3. 把对象指向这个空间
                 */
                    s = new Single();
            }
        }
        return s;
    }
}


/**
 * 多线程环境下的懒汉式单例模式(DCL，双检锁+volatile实现)
 * 加入了volatile变量来禁止指令重排序
 * @author ywq
 */
class Single4{
    private Single4(){}
    private static volatile Single s = null;

    public static  Single getInstance(){
        if(null==s){
            synchronized(Single.class){
                if(null==s)
                    s = new Single();
            }
        }
        return s;
    }
}
```

#### 多线程设计

**用 thread来构造多线程**

```java
public class myThread{
    public static void main(String[] args) {
        my_thread myth1 = new my_thread("th01");
        my_thread myth2 = new my_thread("th02");
        my_thread myth3 = new my_thread("th03");
        myth1.start();
        myth2.start();
        myth3.start();
    }
    public static class my_thread extends Thread{
        private String name;
        public my_thread (String name){
            this.name = name;
        }
        @Override
        public void run(){
            for (int i = 0; i<10 ; i++){
                System.out.println(this.name + ":  i = " + i);
            }
        }
    }
```

**用 runnable 来构造多线程**

```java
    public static void main(String[] args) {
        Thread ru01 = new Thread(new my_Runnable("ru01"));
        Thread ru02 = new Thread(new my_Runnable("ru02"));
        Thread ru03 = new Thread(new my_Runnable("ru03"));
        ru01.start();
        ru02.start();
        ru03.start();

    }
    public static class my_Runnable implements Runnable{
        private String name;
        public my_Runnable(String name){
            this.name = name;
        }
        @Override
        public void run() {
            for (int i = 0; i<5; i++){
                System.out.println(this.name+"  :i="+i);
            }
        }
    }
}
```

**Callable 创建线程代码**：

```java
public class CallableTest {
    public static void main(String[] args) {
        Callable1 c = new Callable1();

        //异步计算的结果
        FutureTask<Integer> result = new FutureTask<>(c);

        new Thread(result).start();

        try {
            //等待任务完成，返回结果
            int sum = result.get();
            System.out.println(sum);
        } catch (InterruptedException | ExecutionException e) {
            e.printStackTrace();
        }
    }

}

class Callable1 implements Callable<Integer> {

    @Override
    public Integer call() throws Exception {
        int sum = 0;

        for (int i = 0; i <= 100; i++) {
            sum += i;
        }
        return sum;
    }
}
```

**使用 Executors 创建线程代码**：

```java
public class ExecutorsTest {
    public static void main(String[] args) {
        //获取ExecutorService实例，生产禁用，需要手动创建线程池
        ExecutorService executorService = Executors.newCachedThreadPool();
        //提交任务
        executorService.submit(new RunnableDemo());
    }
}

class RunnableDemo implements Runnable {
    @Override
    public void run() {
        System.out.println("大彬");
    }
}
```

#### java实现死锁

```java
import java.util.concurrent.TimeUnit;

/**
 * 资源类
 */
class HoldLockThread implements Runnable{

    private String lockA;
    private String lockB;

    // 持有自己的锁，还想得到别人的锁

    public HoldLockThread(String lockA, String lockB) {
        this.lockA = lockA;
        this.lockB = lockB;
    }


    @Override
    public void run() {
        synchronized (lockA) {
            System.out.println(Thread.currentThread().getName() + "\t 自己持有" + lockA + "\t 尝试获取：" + lockB);

            try {
                TimeUnit.SECONDS.sleep(2);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }

            synchronized (lockB) {
                System.out.println(Thread.currentThread().getName() + "\t 自己持有" + lockB + "\t 尝试获取：" + lockA);
            }
        }
    }
}
public class DeadLockDemo {
    public static void main(String[] args) {
        String lockA = "lockA";
        String lockB = "lockB";

        new Thread(new HoldLockThread(lockA, lockB), "t1").start();

        new Thread(new HoldLockThread(lockB, lockA), "t2").start();
    }
}
```

#### 多线程卖票

~~~java
```java
package niuke.thread;

public class WindowTicket {

    public static void main(String[] args) {

        TicketSale ticketSale = new TicketSale();
        Thread Sale1 = new Thread(ticketSale, "售票口1");
        Thread Sale2 = new Thread(ticketSale, "售票口2");
        Thread Sale3 = new Thread(ticketSale, "售票口3");
        Thread Sale4 = new Thread(ticketSale, "售票口4");
        // 启动线程，开始售票
        Sale1.start();
        Sale2.start();
        Sale3.start();
        Sale4.start();
    }
}

class TicketSale implements Runnable {
    int ticketSum = 100;

    @Override
    public void run() {
        try {
            Thread.sleep(100);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        // 有余票，就卖
        while (ticketSum > 0) {
            System.out.println(Thread.currentThread().getName() + "售出第" + (100 - ticketSum + 1) + "张票");
            ticketSum--;
        }
        System.out.println(Thread.currentThread().getName() + "表示没有票了");
    }
}

```

~~~

#### **交替打印线程**

方法一：volatile标记flag变量

```java
public class Main {

   private static volatile int state=0;

    public static void main(String[] args) {
        new Thread(()->{
          for(int i=0;i<100;)
          {
              if(state%3==0)
              {
                  System.out.println("A");
                  state++;
                  i++;
              }
          }
        },"A").start();
        new Thread(()->{
            for(int i=0;i<100;)
            {
                if(state%3==1)
                {
                    System.out.println("B");
                    state++;
                    i++;
                }
            }
        },"B").start();
        new Thread(()->{
            for(int i=0;i<100;)
            {
                if(state%3==2)
                {
                    System.out.println("C");
                    state++;
                    i++;
                }
            }
        },"C").start();
    }
}
```

```java
// 方法二：sychronized加锁通知等待
public class B {
    static final Object ob=new Object();
    static int num=1;
    public static void main(String[] args) {
        new Thread(()->{
            synchronized (ob)
            {
                while (num<=100)
                {
                    //偶数等待
                    if(num%2==0)
                    {
                        try {
                            ob.wait();
                        } catch (InterruptedException e) {
                            e.printStackTrace();
                        }
                    }
                    else
                    {
                        System.out.println(Thread.currentThread().getName()+":"+num++);
                        ob.notify();
                    }
                }
            }
        },"A").start();
        new Thread(()->{
            synchronized (ob)
            {
                while (num<=100)
                {
                    //打印偶数 基数线程等待
                 if(num%2!=0) {
                     try {
                         ob.wait();
                     } catch (InterruptedException e) {
                         e.printStackTrace();
                     }
                 }
                 else
                 {
                     System.out.println(Thread.currentThread().getName()+":"+num++);
                     ob.notify();
                 }
                }
            }
        },"B").start();
    }
}
```

#### 奇偶交替打印

```java
public class Main {

   private static volatile int state=0;

    public static void main(String[] args) {
        new Thread(()->{
          for(int i=0;i<100;)
          {
              if(state%3==0)
              {
                  System.out.println("A");
                  state++;
                  i++;
              }
          }
        },"A").start();
        new Thread(()->{
            for(int i=0;i<100;)
            {
                if(state%3==1)
                {
                    System.out.println("B");
                    state++;
                    i++;
                }
            }
        },"B").start();
        new Thread(()->{
            for(int i=0;i<100;)
            {
                if(state%3==2)
                {
                    System.out.println("C");
                    state++;
                    i++;
                }
            }
        },"C").start();
    }
}
```

## 系统设计

#### 扫码登录



#### 抢红包



#### 短网址



#### 朋友圈

#### 

 

## [大数据](https://mp.weixin.qq.com/s?__biz=MzU1NTA0NTEwMg==&mid=2247483860&idx=1&sn=e211f83b5fea6abc87c724579a28a883&chksm=fbdb1855ccac914371ba9f7da9db2f072964c1eada5176312a00eb7d19522954a0bff0f0e1f7&scene=21#wechat_redirect)

关键点：分而治之，常用hashmap和bitmap

#### 10 亿个IP进行排序

先转化成十进制，然后放入bitmap

#### 10 亿个年龄排序

用一个200大的数组hash统计

#### 2G内存在20亿个32位大整数中找到出现次数最多的数

哈希需要20亿*8字节=16G，因此进行哈希分流到8个机器

#### 10M内存找到40亿个数中没有的自然数

bitmap需要500m内存，因此分区间，2^32/64,找到不满的区间再进行bitmap填充

#### 百亿单次找到最热的100词

分流，堆，外部排序

#### 一致性哈希算法

![把一致性哈希算法原理讲的最清楚的一篇- 知乎](https://pic4.zhimg.com/v2-2f6bd808d11171fa3ae9accf6927e107_b.jpg)

**布隆过滤器** 特点： 网页黑名单系统，垃圾邮件过滤系统，爬虫的网址判断重复系统，容忍一定程度的失误率，对空间要求较严格

![img](https://user-gold-cdn.xitu.io/2019/11/30/16eba60985ae27ec?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

•如何从大量的 URL 中找出相同的 URL？（百度）

•如何从大量数据中找出高频词？（百度）

•如何找出某一天访问百度网站最多的 IP？（百度）

•如何在大量的数据中找出不重复的整数？（百度）

•如何在大量的数据中判断一个数是否存在？（腾讯）

•如何查询最热门的查询串？（腾讯）

•如何统计不同电话号码的个数？（百度）

•如何从 5 亿个数中找出中位数？（百度）

•如何按照 query 的频度排序？（百度）

•如何找出排名前 500 的数？（腾讯）

答案呢？**往下看~**

题目1

### 题目描述

给定 a、b 两个文件，各存放 50 亿个 URL，每个 URL 各占 64B，内存限制是 4G。请找出 a、b 两个文件共同的 URL。

### 解答思路

每个 URL 占 64B，那么 50 亿个 URL占用的空间大小约为 320GB。

> 5,000,000,000 \* 64B ≈ 5GB \* 64 = 320GB

由于内存大小只有 4G，因此，我们不可能一次性把所有 URL 加载到内存中处理。对于这种类型的题目，一般采用**分治策略**，即：把一个文件中的 URL 按照某个特征划分为多个小文件，使得每个小文件大小不超过 4G，这样就可以把这个小文件读到内存中进行处理了。

**思路如下**：

首先遍历文件 a，对遍历到的 URL 求 `hash(URL) % 1000`，根据计算结果把遍历到的  URL 存储到文件  a0, a1, a2, ..., a999，这样每个大小约为 300MB。使用同样的方法遍历文件 b，把文件 b 中的 URL 分别存储到文件 b0, b1, b2, ..., b999 中。这样处理过后，所有可能相同的 URL 都在对应的小文件中，即 a0 对应 b0, ..., a999 对应 b999，不对应的小文件不可能有相同的 URL。那么接下来，我们只需要求出这 1000 对小文件中相同的 URL 就好了。

接着遍历 ai( `i∈[0,999]`)，把 URL 存储到一个 HashSet 集合中。然后遍历 bi 中每个 URL，看在 HashSet 集合中是否存在，若存在，说明这就是共同的 URL，可以把这个 URL 保存到一个单独的文件中。

### 方法总结

1.分而治之，进行哈希取余；2.对每个子文件进行 HashSet 统计。

#### 题目2

### 题目描述

有一个 1GB 大小的文件，文件里每一行是一个词，每个词的大小不超过 16B，内存大小限制是 1MB，要求返回频数最高的 100 个词(Top 100)。

### 解答思路

由于内存限制，我们依然无法直接将大文件的所有词一次读到内存中。因此，同样可以采用**分治策略**，把一个大文件分解成多个小文件，保证每个文件的大小小于 1MB，进而直接将单个小文件读取到内存中进行处理。

**思路如下**：

首先遍历大文件，对遍历到的每个词x，执行 `hash(x) % 5000`，将结果为 i 的词存放到文件 ai 中。遍历结束后，我们可以得到 5000 个小文件。每个小文件的大小为 200KB 左右。如果有的小文件大小仍然超过 1MB，则采用同样的方式继续进行分解。

接着统计每个小文件中出现频数最高的 100 个词。最简单的方式是使用 HashMap 来实现。其中 key 为词，value 为该词出现的频率。具体方法是：对于遍历到的词 x，如果在 map 中不存在，则执行 `map.put(x, 1)`；若存在，则执行 `map.put(x, map.get(x)+1)`，将该词频数加 1。

上面我们统计了每个小文件单词出现的频数。接下来，我们可以通过维护一个**小顶堆**来找出所有词中出现频数最高的 100 个。具体方法是：依次遍历每个小文件，构建一个**小顶堆**，堆大小为 100。如果遍历到的词的出现次数大于堆顶词的出现次数，则用新词替换堆顶的词，然后重新调整为**小顶堆**，遍历结束后，小顶堆上的词就是出现频数最高的 100 个词。

### 方法总结

1.分而治之，进行哈希取余；2.使用 HashMap 统计频数；3.求解**最大**的 TopN 个，用**小顶堆**；求解**最小**的 TopN 个，用**大顶堆**。

#### 题目3

### 题目描述

现有海量日志数据保存在一个超大文件中，该文件无法直接读入内存，要求从中提取某天访问百度次数最多的那个 IP。

### 解答思路

这道题只关心某一天访问百度最多的 IP，因此，可以首先对文件进行一次遍历，把这一天访问百度 IP 的相关信息记录到一个单独的大文件中。接下来采用的方法与上一题一样，大致就是先对 IP 进行哈希映射，接着使用 HashMap 统计重复 IP 的次数，最后计算出重复次数最多的 IP。

> 注：这里只需要找出出现次数最多的 IP，可以不必使用堆，直接用一个变量 max 即可。

### 方法总结

1.分而治之，进行哈希取余；2.使用 HashMap 统计频数；3.求解**最大**的 TopN 个，用**小顶堆**；求解**最小**的 TopN 个，用**大顶堆**。

#### 题目4

### 题目描述

在 2.5 亿个整数中找出不重复的整数。注意：内存不足以容纳这 2.5 亿个整数。

### 解答思路

#### 方法一：分治法

与前面的题目方法类似，先将 2.5 亿个数划分到多个小文件，用 HashSet/HashMap 找出每个小文件中不重复的整数，再合并每个子结果，即为最终结果。

#### 方法二：位图法

**位图**，就是用一个或多个 bit 来标记某个元素对应的值，而键就是该元素。采用位作为单位来存储数据，可以大大节省存储空间。

位图通过使用位数组来表示某些元素是否存在。它可以用于快速查找，判重，排序等。不是很清楚？我先举个小例子。

假设我们要对 `[0,7]` 中的 5 个元素 (6, 4, 2, 1, 5) 进行排序，可以采用位图法。0~7 范围总共有 8 个数，只需要 8bit，即 1 个字节。首先将每个位都置 0：

然后遍历 5 个元素，首先遇到 6，那么将下标为 6 的位的 0 置为 1；接着遇到 4，把下标为 4 的位 的 0 置为 1：

依次遍历，结束后，位数组是这样的：

每个为 1 的位，它的下标都表示了一个数：

这样我们其实就已经实现了排序。

对于整数相关的算法的求解，**位图法**是一种非常实用的算法。假设 int 整数占用 4B，即 32bit，那么我们可以表示的整数的个数为 232。

**那么对于这道题**，我们用 2 个 bit 来表示各个数字的状态：

•00 表示这个数字没出现过；•01 表示这个数字出现过一次（即为题目所找的不重复整数）；•10 表示这个数字出现了多次。

那么这 232 个整数，总共所需内存为 232\*2b=1GB。因此，当可用内存超过 1GB 时，可以采用位图法。假设内存满足位图法需求，进行下面的操作：

遍历 2.5 亿个整数，查看位图中对应的位，如果是 00，则变为 01，如果是 01 则变为 10，如果是 10 则保持不变。遍历结束后，查看位图，把对应位是 01 的整数输出即可。

### 方法总结

**判断数字是否重复的问题**，位图法是一种非常高效的方法。

#### 题目5

### 题目描述

给定 40 亿个不重复的没排过序的 unsigned int 型整数，然后再给定一个数，如何快速判断这个数是否在这 40 亿个整数当中？

### 解答思路

#### 方法一：分治法

依然可以用分治法解决，方法与前面类似，就不再次赘述了。

#### 方法二：位图法

40 亿个不重复整数，我们用 40 亿个 bit 来表示，初始位均为 0，那么总共需要内存：4,000,000,000b≈512M。

我们读取这 40 亿个整数，将对应的 bit 设置为 1。接着读取要查询的数，查看相应位是否为 1，如果为 1 表示存在，如果为 0 表示不存在。

### 方法总结

**判断数字是否存在、判断数字是否重复的问题**，位图法是一种非常高效的方法。

#### 题目6

### 题目描述

搜索引擎会通过日志文件把用户每次检索使用的所有查询串都记录下来，每个查询床的长度不超过 255 字节。

假设目前有 1000w 个记录（这些查询串的重复度比较高，虽然总数是 1000w，但如果除去重复后，则不超过 300w 个）。请统计最热门的 10 个查询串，要求使用的内存不能超过 1G。（一个查询串的重复度越高，说明查询它的用户越多，也就越热门。）

### 解答思路

每个查询串最长为 255B，1000w 个串需要占用 约 2.55G 内存，因此，我们无法将所有字符串全部读入到内存中处理。

#### 方法一：分治法

分治法依然是一个非常实用的方法。

划分为多个小文件，保证单个小文件中的字符串能被直接加载到内存中处理，然后求出每个文件中出现次数最多的 10 个字符串；最后通过一个小顶堆统计出所有文件中出现最多的 10 个字符串。

方法可行，但不是最好，下面介绍其他方法。

#### 方法二：HashMap 法

虽然字符串总数比较多，但去重后不超过 300w，因此，可以考虑把所有字符串及出现次数保存在一个 HashMap 中，所占用的空间为 300w\*(255+4)≈777M（其中，4表示整数占用的4个字节）。由此可见，1G 的内存空间完全够用。

**思路如下**：

首先，遍历字符串，若不在 map 中，直接存入 map，value 记为 1；若在 map 中，则把对应的 value 加 1，这一步时间复杂度 `O(N)`。

接着遍历 map，构建一个 10 个元素的小顶堆，若遍历到的字符串的出现次数大于堆顶字符串的出现次数，则进行替换，并将堆调整为小顶堆。

遍历结束后，堆中 10 个字符串就是出现次数最多的字符串。这一步时间复杂度 `O(Nlog10)`。

#### 方法三：前缀树法

方法二使用了 HashMap 来统计次数，当这些字符串有大量相同前缀时，可以考虑使用前缀树来统计字符串出现的次数，树的结点保存字符串出现次数，0 表示没有出现。

**思路如下**：

在遍历字符串时，在前缀树中查找，如果找到，则把结点中保存的字符串次数加 1，否则为这个字符串构建新结点，构建完成后把叶子结点中字符串的出现次数置为 1。

最后依然使用小顶堆来对字符串的出现次数进行排序。

### 方法总结

前缀树经常被用来统计字符串的出现次数。它的另外一个大的用途是字符串查找，判断是否有重复的字符串等。

#### 题目7

### 题目描述

已知某个文件内包含一些电话号码，每个号码为 8 位数字，统计不同号码的个数。

### 解答思路

这道题本质还是求解**数据重复**的问题，对于这类问题，一般首先考虑位图法。

对于本题，8 位电话号码可以表示的号码个数为 108 个，即 1 亿个。我们每个号码用一个 bit 来表示，则总共需要 1 亿个 bit，内存占用约 100M。

**思路如下**：

申请一个位图数组，长度为 1 亿，初始化为 0。然后遍历所有电话号码，把号码对应的位图中的位置置为 1。遍历完成后，如果 bit 为 1，则表示这个电话号码在文件中存在，否则不存在。bit 值为 1 的数量即为 不同电话号码的个数。

### 方法总结

求解数据重复问题，记得考虑位图法。

#### 题目8

### 题目描述

从 5 亿个数中找出中位数。数据排序后，位置在最中间的数就是中位数。当样本数为奇数时，中位数为 第 `(N+1)/2` 个数；当样本数为偶数时，中位数为 第 `N/2` 个数与第 `1+N/2` 个数的均值。

### 解答思路

如果这道题没有内存大小限制，则可以把所有数读到内存中排序后找出中位数。但是最好的排序算法的时间复杂度都为 `O(NlogN)`。这里使用其他方法。

#### 方法一：双堆法

维护两个堆，一个大顶堆，一个小顶堆。大顶堆中最大的数**小于等于**小顶堆中最小的数；保证这两个堆中的元素个数的差不超过 1。

若数据总数为**偶数**，当这两个堆建好之后，**中位数就是这两个堆顶元素的平均值**。当数据总数为**奇数**时，根据两个堆的大小，**中位数一定在数据多的堆的堆顶**。

> 见 LeetCode No.295：https://leetcode.com/problems/find-median-from-data-stream/

以上这种方法，需要把所有数据都加载到内存中。当数据量很大时，就不能这样了，因此，这种方法**适用于数据量较小的情况**。5 亿个数，每个数字占用 4B，总共需要 2G 内存。如果可用内存不足 2G，就不能使用这种方法了，下面介绍另一种方法。

#### 方法二：分治法

分治法的思想是把一个大的问题逐渐转换为规模较小的问题来求解。

对于这道题，顺序读取这  5  亿个数字，对于读取到的数字  num，如果它对应的二进制中最高位为 1，则把这个数字写到  f1  中，否则写入  f0  中。通过这一步，可以把这  5  亿个数划分为两部分，而且  f0  中的数都大于  f1  中的数（最高位是符号位）。

划分之后，可以非常容易地知道中位数是在 f0 还是 f1 中。假设 f1 中有 1 亿个数，那么中位数一定在 f0 中，且是在 f0 中，从小到大排列的第 1.5 亿个数与它后面的一个数的平均值。

> **提示**，5 亿数的中位数是第 2.5 亿与右边相邻一个数求平均值。若 f1 有一亿个数，那么中位数就是 f0 中从第 1.5 亿个数开始的两个数求得的平均值。

对于 f0 可以用次高位的二进制继续将文件一分为二，如此划分下去，直到划分后的文件可以被加载到内存中，把数据加载到内存中以后直接排序，找出中位数。

> **注意**，当数据总数为偶数，如果划分后两个文件中的数据有相同个数，那么中位数就是数据较小的文件中的最大值与数据较大的文件中的最小值的平均值。

### 方法总结

分治法，真香！

#### 题目9

### 题目描述

有 10 个文件，每个文件大小为 1G，每个文件的每一行存放的都是用户的 query，每个文件的 query 都可能重复。要求按照 query 的频度排序。

### 解答思路

如果 query 的重复度比较大，可以考虑一次性把所有 query 读入内存中处理；如果 query 的重复率不高，那么可用内存不足以容纳所有的 query，这时候就需要采用分治法或其他的方法来解决。

#### 方法一：HashMap 法

如果 query 重复率高，说明不同 query 总数比较小，可以考虑把所有的 query 都加载到内存中的 HashMap 中。接着就可以按照 query 出现的次数进行排序。

#### 方法二：分治法

分治法需要根据数据量大小以及可用内存的大小来确定问题划分的规模。对于这道题，可以顺序遍历 10 个文件中的 query，通过 Hash 函数 `hash(query) % 10` 把这些 query 划分到 10 个小文件中。之后对每个小文件使用 HashMap 统计 query 出现次数，根据次数排序并写入到零外一个单独文件中。

接着对所有文件按照 query 的次数进行排序，这里可以使用归并排序（由于无法把所有 query 都读入内存，因此需要使用外排序）。

### 方法总结

•内存若够，直接读入进行排序；•内存不够，先划分为小文件，小文件排好序后，整理使用外排序进行归并。

#### 题目10

### 题目描述

有 20 个数组，每个数组有 500 个元素，并且有序排列。如何在这 20\*500 个数中找出前 500 的数？

### 解答思路

对于 TopK 问题，最常用的方法是使用堆排序。对本题而言，假设数组降序排列，可以采用以下方法：

首先建立大顶堆，堆的大小为数组的个数，即为 20，把每个数组最大的值存到堆中。

接着删除堆顶元素，保存到另一个大小为 500 的数组中，然后向大顶堆插入删除的元素所在数组的下一个元素。

重复上面的步骤，直到删除完第 500 个元素，也即找出了最大的前 500 个数。

> 为了在堆中取出一个数据后，能知道它是从哪个数组中取出的，从而可以从这个数组中取下一个值，可以把数组的指针存放到堆中，对这个指针提供比较大小的方法。

```
import lombok.Data;

import java.util.Arrays;
import java.util.PriorityQueue;

/**
 * @author https://github.com/yanglbme
 */
@Data
public class DataWithSource implements Comparable<DataWithSource> {
    /**
     * 数值
     */
    private int value;

    /**
     * 记录数值来源的数组
     */
    private int source;

    /**
     * 记录数值在数组中的索引
     */
    private int index;

    public DataWithSource(int value, int source, int index) {
        this.value = value;
        this.source = source;
        this.index = index;
    }

    /**
     *
     * 由于 PriorityQueue 使用小顶堆来实现，这里通过修改
     * 两个整数的比较逻辑来让 PriorityQueue 变成大顶堆
     */
    @Override
    public int compareTo(DataWithSource o) {
        return Integer.compare(o.getValue(), this.value);
    }
}


class Test {
    public static int[] getTop(int[][] data) {
        int rowSize = data.length;
        int columnSize = data[0].length;

        // 创建一个columnSize大小的数组，存放结果
        int[] result = new int[columnSize];

        PriorityQueue<DataWithSource> maxHeap = new PriorityQueue<>();
        for (int i = 0; i < rowSize; ++i) {
            // 将每个数组的最大一个元素放入堆中
            DataWithSource d = new DataWithSource(data[i][0], i, 0);
            maxHeap.add(d);
        }

        int num = 0;
        while (num < columnSize) {
            // 删除堆顶元素
            DataWithSource d = maxHeap.poll();
            result[num++] = d.getValue();
            if (num >= columnSize) {
                break;
            }

            d.setValue(data[d.getSource()][d.getIndex() + 1]);
            d.setIndex(d.getIndex() + 1);
            maxHeap.add(d);
        }
        return result;

    }

    public static void main(String[] args) {
        int[][] data = {
                {29, 17, 14, 2, 1},
                {19, 17, 16, 15, 6},
                {30, 25, 20, 14, 5},
        };

        int[] top = getTop(data);
        System.out.println(Arrays.toString(top)); // [30, 29, 25, 20, 19]
    }
}
```

### 方法总结

求 TopK，不妨考虑一下堆排序？

## [智力题](https://mp.weixin.qq.com/s?__biz=MzU1NTA0NTEwMg==&mid=2247483985&idx=1&sn=5cd8587506ea5b6dd7bebfbb00db94ed&chksm=fbdb1bd0ccac92c608fd8cc41f4500ff0a385b6c8c21a6ada45de5570669ce18d6414540c011&scene=21#wechat_redirect)

#### 狼吃羊

狼为奇数：吃

狼为偶数：不吃

#### 烧绳子

开始时一根香两头点着，一根香只点一头，两头点着的绳子烧完说明过去了半小时，这时将只点了一头的绳子另一头也点着，从这时开始到烧完就是15分钟。

#### 倒水

> **不断用小桶装水倒入大桶，大桶满了立即清空，每次判断下二个桶中水的容量是否等于指定容量。**

#### 坐标系中有一个球桌，四个角坐标：(0,0), (0,4), (2,4), (2,0)一颗球在(1,1)，请问从哪些角度可以射入洞内（可无限次碰撞）？

一般想法是将球镜像对称，但这道题是把洞镜像对称将这个桌面在这个平面无限延展，可类比成无限张球桌紧密放置那么每一个和球洞的连线都是合法路径

#### 11223344排列问题

带技巧的穷举，先排列4，然后321

## 高频智力题

### **1. 高楼扔鸡蛋问题**

有一栋楼共`**100**`层，一个鸡蛋从第`**N**`层及以上的楼层落下来会摔破， 在第`**N**`层以下的楼层落下不会摔破。给你`**2**`个鸡蛋，如何用最少的尝试次数，测试出鸡蛋不会摔碎的临界点？

<details class="notion-toggle notion-block-e73ea2006387440b8510e04ad29bf36a" open="" style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 3px 2px;"><summary style="box-sizing: border-box; margin-block: 0px; outline: none; cursor: pointer; color: var(--theme-color,#42b983); font-weight: 700; font-size: 20px !important;"></summary><div style="box-sizing: border-box; margin-block: 0px; outline: 0px; margin-left: 1.1em;"><div class="notion-text notion-block-7dfbcffd9ed04fdcb593ec7470abcefb" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 2px 0px 1px;">首先要说明的是这道题你要是一上来就说出正确答案，那说明你的智商不是超过160就是你做过这题。</div><div class="notion-text notion-block-eed58f4099fb4749be33c2e4402fc93e" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">所以建议你循序渐进的回答，一上来就说最优解可能结果不会让面试官满意。</div><div class="notion-text notion-block-7427ed736ec444049d5f9c7c3659a67c" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">1. 暴力法</b></div><div class="notion-text notion-block-8483fff4db71498d9bfbe56b4d115054" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">从<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">1</b></code>到<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">100</b></code>，一层一层试。在最坏情况下，这个方法需要扔<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">100</b></code>次。 这个办法太蠢了，完全用不上两个鸡蛋这个条件，不建议回答这个方法。</div><div class="notion-text notion-block-ff4d8b17353c4dff9634f0a6d44d85da" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">2. 二分法</b></div><div class="notion-text notion-block-d88ba2dd667441a3b0134be68d23d05a" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">采用类似于二分查找的方法，把鸡蛋从一半楼层（<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">50</b></code>层）往下扔。</div><ul class="notion-list notion-list-disc notion-block-d30226aed5a6487a859af4ae853be965" style="box-sizing: border-box; margin-block: 0.6em; outline: 0px; margin: 0px; list-style-type: disc; padding-inline-start: 1.7em;"><li style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 6px 0px; white-space: pre-wrap;">如果第一枚鸡蛋，在<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">50</b></code>层碎了，第二枚鸡蛋，就从第<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">1</b></code>层开始扔，一层一层增长，一直扔到第<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">49</b></code>层。</li></ul><ul class="notion-list notion-list-disc notion-block-f83b37a691c84be8a015d1a1f14e8512" style="box-sizing: border-box; margin-block: 0.6em; outline: 0px; margin: 0px; list-style-type: disc; padding-inline-start: 1.7em;"><li style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 6px 0px; white-space: pre-wrap;">如果第一枚鸡蛋在<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">50</b></code>层没碎，则继续使用二分法，在剩余楼层的一半（<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">75</b></code>层）往下扔......</li></ul><div class="notion-text notion-block-5fd7c90e9c4649ebbbbc4eb132e2edab" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">这个方法在最坏情况下，需要尝试<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">50</b></code>次。</div><div class="notion-text notion-block-c0bc768ca99e4e878bf5410666218130" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">3. 均匀法</b></div><div class="notion-text notion-block-07a38465dc714b1b854ac15a034c246b" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">如何让第一枚鸡蛋和第二枚鸡蛋的尝试次数，尽可能均衡呢？</div><div class="notion-text notion-block-d5f727f732784df98f9b7ce05105c146" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">很简单，做一个平方根运算，<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">100</b></code>的平方根是<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">10</b></code>。</div><div class="notion-text notion-block-9fa37de4f2fb4236afc6ca1d37cfde4f" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">因此，我们尝试每<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">10</b></code>层扔一次，第一次从<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">10</b></code>层扔，第二次从<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">20</b></code>层扔，第三次从<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">30</b></code>层......一直扔到<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">100</b></code>层。</div><div class="notion-text notion-block-4068d2542e6542d690c3ebd2d13f09da" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">这样的最好情况是在第<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">10</b></code>层碎掉，尝试次数为&nbsp;<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">1 + 9 = 10</b></code>次。</div><div class="notion-text notion-block-d176111578e64e79a992494b9d306919" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">最坏的情况是在第<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">100</b></code>层碎掉，尝试次数为&nbsp;<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">10 + 9 = 19</b></code>次。</div><div class="notion-text notion-block-13fb330cf4db40a7abe3ff3ea8f9d6f6" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">不过，这里有一个小小的优化点，我们可以从<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">15</b></code>层开始扔，接下来从<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">25</b></code>层、<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">35</b></code>层扔......一直到<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">95</b></code>层。</div><div class="notion-text notion-block-90c18385f3b44180991168352908f724" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">这样最坏情况是在第<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">95</b></code>层碎掉，尝试次数为&nbsp;<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">9 + 9 = 18</b></code>次。</div><div class="notion-text notion-block-ad45f0c12a5648db9d49c4bfded423fd" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">4. 最优解法</b></div><div class="notion-text notion-block-80bf2cc1cc574ec98a592c475292ca7d" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">最优解法是反向思考的经典：如果最优解法在最坏情况下需要扔<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">X</b></code>次，那第一次在第几层扔最好呢？</div><div class="notion-text notion-block-0723209cd8564a51a182e8a02475894c" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">答案是：从</b><code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">X</b></code><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">层扔</b></div><div class="notion-text notion-block-2f7c85ca5d4e46e797bfa2a438f21374" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">假设最优的尝试次数的<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">x</b></code>次，为什么第一次扔就要选择第<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">x</b></code>层呢？</div><div class="notion-text notion-block-aff99d32eb534eea96ffb147d6d112db" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">这里的解释会有些烧脑，请小伙伴们坐稳扶好：</div><ul class="notion-list notion-list-disc notion-block-3df9f57daa4c4517be9f3472a6573a7c" style="box-sizing: border-box; margin-block: 0.6em; outline: 0px; margin: 0px; list-style-type: disc; padding-inline-start: 1.7em;"><li style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 6px 0px; white-space: pre-wrap;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">假设第一次扔在第</b><code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">x+1</b></code><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">层：</b></li></ul><div class="notion-text notion-block-6be02769db3d46b3bce2ad8e42e1c3e7" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">如果第一个鸡蛋碎了，那么第二个鸡蛋只能从第1层开始一层一层扔，一直扔到第x层。</div><div class="notion-text notion-block-b3cd86c16adc468f883f7859fb8411af" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">这样一来，我们总共尝试了<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">x+1</b></code>次，和假设尝试<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">x</b></code>次相悖。由此可见，第一次扔的楼层必须小于<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">x+1</b></code>层。</div><ul class="notion-list notion-list-disc notion-block-fa3d1acbdd0444baa10a513b4d71fe68" style="box-sizing: border-box; margin-block: 0.6em; outline: 0px; margin: 0px; list-style-type: disc; padding-inline-start: 1.7em;"><li style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 6px 0px; white-space: pre-wrap;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">假设第一次扔在第</b><code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">x-1</b></code><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">层：</b></li></ul><div class="notion-text notion-block-6e5d4b15e00f410da8510026eb25f0f1" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">如果第一个鸡蛋碎了，那么第二个鸡蛋只能从第<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">1</b></code>层开始一层一层扔，一直扔到第<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">x-2</b></code>层。</div><div class="notion-text notion-block-06d8659779c3439b866e302f153e585e" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">这样一来，我们总共尝试了<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">x-2+1 = x-1</b></code>次，虽然没有超出假设次数，但似乎有些过于保守。</div><ul class="notion-list notion-list-disc notion-block-4fd1b48c5ebe4fe0875cfde01b60c5b1" style="box-sizing: border-box; margin-block: 0.6em; outline: 0px; margin: 0px; list-style-type: disc; padding-inline-start: 1.7em;"><li style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 6px 0px; white-space: pre-wrap;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">假设第一次扔在第</b><code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">x</b></code><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">层：</b></li></ul><div class="notion-text notion-block-354331ea2bc94882a7a8763b14fc6d4f" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">如果第一个鸡蛋碎了，那么第二个鸡蛋只能从第<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">1</b></code>层开始一层一层扔，一直扔到第<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">x-1</b></code>层。</div><div class="notion-text notion-block-4c708dac486642ef9a5c94a75186fbf8" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">这样一来，我们总共尝试了<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">x-1+1 = x</b></code>次，刚刚好没有超出假设次数。</div><div class="notion-text notion-block-923b719b81f849f3857648a88149449d" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">因此，要想尽量楼层跨度大一些，又要保证不超过假设的尝试次数x，那么第一次扔鸡蛋的最优选择就是第<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">x</b></code>层。</div><div class="notion-text notion-block-b70255a647e44f158e9b48ec43b6467d" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">那么算最坏情况，第二次你只剩下<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">x-1</b></code>次机会，按照上面的说法，你第二次尝试的位置必然是<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">X +（X-1）</b></code>；</div><div class="notion-text notion-block-efd2707329c54055b85843869d28c2da" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">以此类推我们可得：</div><div class="notion-text notion-block-46c380ff05a54d2c9aa321189c1a550b" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;"><code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">x + (x-1) + (x-2) + ... + 1 = 100</b></code></div><div class="notion-text notion-block-81f2a490dc5c41d3875a88f78ca29d7c" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">这个方程不难理解：</div><div class="notion-text notion-block-f2ac81f900f24a549d6283b266f441fd" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">左边的多项式是各次扔鸡蛋的楼层跨度之和。由于假设尝试<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">x</b></code>次，所以这个多项式共有<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">x</b></code>项。</div><div class="notion-text notion-block-d45592a7d1524c0b8dfda1dcb83b94c3" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">右边是总的楼层数<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">100</b></code>。</div><div class="notion-text notion-block-5595c702e81c48a482fc2427b6974f0e" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">下面我们来解这个方程：</div><div class="notion-text notion-block-255d2ec524c84f7882294f8cb6d0f0a4" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;"><code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">x + (x-1) + (x-2) + ... + 1 = 100</b></code>&nbsp;转化为&nbsp;<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">(x+1)*x/2 = 100</b></code></div><div class="notion-text notion-block-5d1fed07df904b6f87f1626ec314ae21" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">最终x向上取整，得到&nbsp;<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">x = 14</b></code></div><div class="notion-text notion-block-6bda887926e448ec89e08d56e710f4bf" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">因此，最优解在最坏情况的尝试次数是<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">14</b></code>次，第一次扔鸡蛋的楼层也是<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">14</b></code>层。</div><div class="notion-text notion-block-0ec834cd14e942d1995be50577699728" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">最后，让我们把第一个鸡蛋没碎的情况下，所尝试的楼层数完整列举出来：</div><div class="notion-text notion-block-6bba3c34b2e3450684b9aa0870af4d26" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;"><code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">14，27， 39， 50， 60， 69， 77， 84， 90， 95， 99， 100</b></code></div><ul class="notion-list notion-list-disc notion-block-2bf5890b915d4b38b942930639031d9e" style="box-sizing: border-box; margin-block: 0.6em; outline: 0px; margin: 0px; list-style-type: disc; padding-inline-start: 1.7em;"><li style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 6px 0px; white-space: pre-wrap;">举个栗子验证下：</li></ul><div class="notion-text notion-block-918abac39f9f495cac15a0fb3bc4803c" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">假如鸡蛋不会碎的临界点是<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">65</b></code>层，那么第一个鸡蛋扔出的楼层是<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">14，27，50，60，69</b></code>。这时候啪的一声碎了。</div><div class="notion-text notion-block-3c7f4e8bea5f4bf69053048dd971228a" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">第二个鸡蛋继续，从<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">61</b></code>层开始，<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">61，62，63，64，65，66</b></code>，啪的一声碎了。</div><div class="notion-text notion-block-6453e91b6e34467984428e1e7ab5a5b5" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">因此得到不会碎的临界点<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">65</b></code>层，总尝试次数是&nbsp;<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">6 + 6 = 12 &lt; 14</b></code>&nbsp;。</div><div class="notion-text notion-block-f79cf0a804f64e9097b32593442e9600" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">下面是我个人的理解：这个更像是优化版的均匀法，均匀法让你第二次尝试不超过<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">10</b></code>，但是第一次的位置无法保证（最多要<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">9</b></code>次，最好一次），这个由于每多一次尝试，楼层间隔就<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">-1</b></code>，最终使得第一次与第二次的和完全均匀（最差情况）。</div><div class="notion-text notion-block-6987b935a13c4513b9fa93a133c40bd6" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">但是核心思路是逆向思考，因为即使理解了需要两次的和均匀也很难得到第一次要在哪层楼扔。</div><div class="notion-text notion-block-90e0ab81f7994dbd8ce2172976f9065a" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">一旦理解了这种方法，多少层楼你都不会怕啦~</div></div></details>

### **2. 找砝码问题**

有一个天平，九个砝码，一个轻一些，用天平至少几次能找到轻的？

<details class="notion-toggle notion-block-bfcff54512ad4c488eb32b5cb6cb0d70" open="" style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 3px 2px;"><summary style="box-sizing: border-box; margin-block: 0px; outline: none; cursor: pointer; color: var(--theme-color,#42b983); font-weight: 700; font-size: 20px !important;"></summary><div style="box-sizing: border-box; margin-block: 0px; outline: 0px; margin-left: 1.1em;"><div class="notion-text notion-block-2b9fcd11406b481686c23d3822cd69c3" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 603.198px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 2px 0px 1px;">三分法。</div><div class="notion-text notion-block-96b4cf7c089c4a24af6187da6de3a9ae" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 603.198px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">答案：2次。</b></div><ul class="notion-list notion-list-disc notion-block-8ca0505f81814518a1ff2628cbf6f359" style="box-sizing: border-box; margin-block: 0.6em; outline: 0px; margin: 0px; list-style-type: disc; padding-inline-start: 1.7em;"><li style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 6px 0px; white-space: pre-wrap;">分三份，两份比较，第三份放一边，如果两份相等质量，则说明轻的在第三份。</li></ul><ul class="notion-list notion-list-disc notion-block-e3f466065a6845859133a5df45dd906a" style="box-sizing: border-box; margin-block: 0.6em; outline: 0px; margin: 0px; list-style-type: disc; padding-inline-start: 1.7em;"><li style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 6px 0px; white-space: pre-wrap;">不论如何，可以确定轻的砝码在某一份的三个之中，再用一次三分法，即可确定。</li></ul></div></details>

### **3. 找玻璃球问题**

有十组玻璃球，每组十个，每个玻璃球重`**10**`g，但其中有一组玻璃球每个只有`**9**`g，给你一个能显示克数的秤，问你最少几次能找到轻的那一组砝码？

<details class="notion-toggle notion-block-d20bc14cb57d433d8a876b43bb2f3fc4" open="" style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 3px 2px;"><summary style="box-sizing: border-box; margin-block: 0px; outline: none; cursor: pointer; color: var(--theme-color,#42b983); font-weight: 700; font-size: 20px !important;"></summary><div style="box-sizing: border-box; margin-block: 0px; outline: 0px; margin-left: 1.1em;"><div class="notion-text notion-block-50da2c76fddb46c69aad8c8c7a0fcfa2" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 599.198px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 2px 0px 1px;">将十组玻璃珠编号<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">1~10</code>，然后第一组拿一个，第二组拿两个以此类推...第十组拿十个
将这些玻璃珠一起放到秤上称出克数<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">x</code>，</div><div class="notion-text notion-block-fcc517a26cc14204ade3c98a6965636c" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 599.198px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">则<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">y = 1*10 + 2*10 + 3*10 + ... + 10 * 10 - x</code></div><div class="notion-text notion-block-6938d281e303414699c550aab6bf4dd2" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 599.198px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">等价于<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">y = (1 + 2 + 3 + ... + 10) * 10 - x = 550 - x</code></div><div class="notion-text notion-block-96c80d49c77d4da0ae4f2f87970541d3" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 599.198px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">第<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">y</code>组就是轻的那组。</div></div></details>


### **4. 毒药问题**

`**1000**`瓶水，其中有一瓶可以无限稀释的毒药，小白鼠喝了毒水就会死（不论含量多低）。要快速找出哪一瓶有毒，需要几只小白鼠？

<details class="notion-toggle notion-block-9415ec64b0144c8397b09ce064d94240" open="" style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 3px 2px;"><summary style="box-sizing: border-box; margin-block: 0px; outline: none; cursor: pointer; color: var(--theme-color,#42b983); font-weight: 700; font-size: 20px !important;"></summary><div style="box-sizing: border-box; margin-block: 0px; outline: 0px; margin-left: 1.1em;"><div class="notion-text notion-block-9481820a9e154103a54e8bb3c09e4943" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 2px 0px 1px;">二进制思路。</div><div class="notion-text notion-block-89b533fad9f142d3998aab17fd88d4a9" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">答：</b><code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">2^10 = 1024 &gt; 1000</b></code><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">，因此</b><code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;"><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">10</b></code><b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">只小白鼠即可。</b></div><div class="notion-text notion-block-2e21295978c64ce79bd6488f7ad3fea8" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">给<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">1000</code>瓶水按照二进制编号，比如<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">3</code>号编为<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">00000 00011</code>，拿<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">10</code>个碗，对应<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">10</code>位，对于<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">3</code>号水来说，最后两位是<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">1</code>，则把水混合进最后两个碗中。
最终把<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">10</code>碗水给对应的小白鼠喝，根据最后小白鼠死亡的情况（死即为<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">1</code>，活即为<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">0</code>），即可确定出有毒的那碗水。</div></div></details>


### **5. 生成随机数问题**

给定生成`**1**`到`**5**`的随机数`**Rand5()**`，如何得到生成`**1**`到`**7**`的随机数函数`**Rand7()**`？

<details class="notion-toggle notion-block-2c2bb75282074c728f44b7a7b8b4b938" open="" style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 3px 2px;"><summary style="box-sizing: border-box; margin-block: 0px; outline: none; cursor: pointer; color: var(--theme-color,#42b983); font-weight: 700; font-size: 20px !important;"></summary><div style="box-sizing: border-box; margin-block: 0px; outline: 0px; margin-left: 1.1em;"><ul class="notion-list notion-list-disc notion-block-1a9e2dff6a9149dd8555ba04c2e412c6" style="box-sizing: border-box; margin-block: 0.6em; outline: 0px; margin: 0px; list-style-type: disc; padding-inline-start: 1.7em;"><li style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 6px 0px; white-space: pre-wrap;">使用 <code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">rand5()</code> 生成 <code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">rand7()</code></li></ul><pre class="notion-code language-java" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 444.594px; padding: 0px; margin: 0.5em 0px 1em; border-radius: 0.375rem; tab-size: 4; display: block; overflow: visible; background: none rgb(253, 253, 253); font-family: Consolas, Monaco, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, monospace; border: 1px solid rgb(229, 231, 235); color: rgb(31, 41, 55); font-size: 13.6px; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; overflow-wrap: normal; line-height: 1.5; hyphens: none; position: relative;"><code class=" language-java" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(31, 41, 55); background: none !important; font-family: Consolas, Monaco, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, monospace; font-size: 1em; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; overflow-wrap: normal; line-height: 1.5; tab-size: 4; hyphens: none; max-height: inherit; height: inherit; padding: 0px !important; display: block; overflow: auto; border: 0px !important; box-shadow: none !important; position: relative;"><span class="token comment" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(91, 155, 76);">// 需要随机得到 1-7</span>
<span class="token keyword" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(59, 130, 246);">public</span> <span class="token keyword" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(59, 130, 246);">static</span> <span class="token keyword" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(59, 130, 246);">int</span> <span class="token function" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(236, 72, 153);">rand7</span><span class="token punctuation" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(55, 65, 81);">(</span><span class="token punctuation" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(55, 65, 81);">)</span> <span class="token punctuation" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(55, 65, 81);">{</span>
    <span class="token keyword" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(59, 130, 246);">while</span> <span class="token punctuation" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(55, 65, 81);">(</span><span class="token boolean" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(16, 185, 129);">true</span><span class="token punctuation" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(55, 65, 81);">)</span> <span class="token punctuation" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(55, 65, 81);">{</span>
      <span class="token keyword" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(59, 130, 246);">int</span> row<span class="token punctuation" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(55, 65, 81);">,</span> col<span class="token punctuation" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(55, 65, 81);">,</span> idx<span class="token punctuation" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(55, 65, 81);">;</span>
      <span class="token comment" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(91, 155, 76);">// rand5() 返回 1-5</span>
      row <span class="token operator" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(245, 158, 11); background: none;">=</span> <span class="token function" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(236, 72, 153);">rand5</span><span class="token punctuation" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(55, 65, 81);">(</span><span class="token punctuation" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(55, 65, 81);">)</span><span class="token punctuation" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(55, 65, 81);">;</span> <span class="token comment" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(91, 155, 76);">// 5 * 5 = 25, 设想一个 5*5 的矩阵</span>
      col <span class="token operator" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(245, 158, 11); background: none;">=</span> <span class="token function" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(236, 72, 153);">rand5</span><span class="token punctuation" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(55, 65, 81);">(</span><span class="token punctuation" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(55, 65, 81);">)</span><span class="token punctuation" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(55, 65, 81);">;</span> <span class="token comment" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(91, 155, 76);">// 然后找到小于25的，7的最大倍数21</span>
      idx <span class="token operator" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(245, 158, 11); background: none;">=</span> col <span class="token operator" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(245, 158, 11); background: none;">+</span> <span class="token punctuation" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(55, 65, 81);">(</span>row <span class="token operator" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(245, 158, 11); background: none;">-</span> <span class="token number" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(16, 185, 129);">1</span><span class="token punctuation" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(55, 65, 81);">)</span> <span class="token operator" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(245, 158, 11); background: none;">*</span> <span class="token number" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(16, 185, 129);">5</span><span class="token punctuation" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(55, 65, 81);">;</span>
      <span class="token keyword" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(59, 130, 246);">if</span> <span class="token punctuation" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(55, 65, 81);">(</span>idx <span class="token operator" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(245, 158, 11); background: none;">&lt;=</span> <span class="token number" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(16, 185, 129);">21</span><span class="token punctuation" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(55, 65, 81);">)</span> <span class="token comment" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(91, 155, 76);">// 只考虑 1-21，划分成 7 份</span>
        <span class="token keyword" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(59, 130, 246);">return</span> <span class="token number" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(16, 185, 129);">1</span> <span class="token operator" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(245, 158, 11); background: none;">+</span> <span class="token punctuation" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(55, 65, 81);">(</span>idx <span class="token operator" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(245, 158, 11); background: none;">-</span> <span class="token number" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(16, 185, 129);">1</span><span class="token punctuation" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(55, 65, 81);">)</span> <span class="token operator" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(245, 158, 11); background: none;">%</span> <span class="token number" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(16, 185, 129);">7</span><span class="token punctuation" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(55, 65, 81);">;</span>
    <span class="token punctuation" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(55, 65, 81);">}</span>
<span class="token punctuation" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(55, 65, 81);">}</span></code></pre></div></details>


### **6. 先手必胜策略问题：**

- `**100**`本书，每次能够拿`**1-5**`本，怎么拿能保证最后一次是你拿？

<details class="notion-toggle notion-block-6d6e1ef3f3ff4c688accb43b732b9e3e" open="" style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 3px 2px;"><summary style="box-sizing: border-box; margin-block: 0px; outline: none; cursor: pointer; color: var(--theme-color,#42b983); font-weight: 700; font-size: 20px !important;"></summary><div style="box-sizing: border-box; margin-block: 0px; outline: 0px; margin-left: 1.1em;"><ul class="notion-list notion-list-disc notion-block-fc687de67c604692b0d6d34620e7cfd6" style="box-sizing: border-box; margin-block: 0.6em; outline: 0px; margin: 0px; list-style-type: disc; padding-inline-start: 1.7em;"><li style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 6px 0px; white-space: pre-wrap;">卡关键点，每次只能拿<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">1</code><code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">5</code>本，所以当剩下<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">6</code>本的时候，不论对面怎么拿你都能赢；</li></ul><ul class="notion-list notion-list-disc notion-block-fdd0440fad1d4655afe5f957badd069c" style="box-sizing: border-box; margin-block: 0.6em; outline: 0px; margin: 0px; list-style-type: disc; padding-inline-start: 1.7em;"><li style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 6px 0px; white-space: pre-wrap;">然后推<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">6</code>的倍数：<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">12、18、...、96</code>，也就是一开始要拿<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">4</code>本；</li></ul><ul class="notion-list notion-list-disc notion-block-896eb75df19d44d78050202c38f4aa29" style="box-sizing: border-box; margin-block: 0.6em; outline: 0px; margin: 0px; list-style-type: disc; padding-inline-start: 1.7em;"><li style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 6px 0px; white-space: pre-wrap;">接下来对面拿<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">1</code>，你就拿<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">5</code>，对面拿<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">2</code>，你就拿<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">4</code>，总之让你拿的和对面拿的加起来是<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">6</code>，最终就能赢。</li></ul></div></details>

- 推广到`**n**`本书，每次拿`**1-k**`本，怎么保证最后一次是你拿？

### **7. 瓶子换饮料问题**

`**1000**`瓶饮料，`**3**`个空瓶子能够换`**1**`瓶饮料，问最多能喝几瓶？

<details class="notion-toggle notion-block-e515da2cee8e427d99159ac9ff836e1f" open="" style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 3px 2px;"><summary style="box-sizing: border-box; margin-block: 0px; outline: none; cursor: pointer; color: var(--theme-color,#42b983); font-weight: 700; font-size: 20px !important;"></summary><div style="box-sizing: border-box; margin-block: 0px; outline: 0px; margin-left: 1.1em;"><ul class="notion-list notion-list-disc notion-block-8fecc0f4a8e449739dd4ad47f67549f8" style="box-sizing: border-box; margin-block: 0.6em; outline: 0px; margin: 0px; list-style-type: disc; padding-inline-start: 1.7em;"><li style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 6px 0px; white-space: pre-wrap;"><code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">1000 % 3 = 333...1</code> 喝掉<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">1000</code>瓶,可以换<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">333</code>瓶汽水, 余<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">1</code>个空瓶</li></ul><ul class="notion-list notion-list-disc notion-block-d185c315a80f47aab39d5dc87cc74e00" style="box-sizing: border-box; margin-block: 0.6em; outline: 0px; margin: 0px; list-style-type: disc; padding-inline-start: 1.7em;"><li style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 6px 0px; white-space: pre-wrap;"><code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">333 % 3 = 111...0</code>　喝掉<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">333</code>瓶，可以换<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">111</code>瓶汽水, 余<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">0</code>个空瓶</li></ul><ul class="notion-list notion-list-disc notion-block-90c3a5f82954423f962dca0d16edca08" style="box-sizing: border-box; margin-block: 0.6em; outline: 0px; margin: 0px; list-style-type: disc; padding-inline-start: 1.7em;"><li style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 6px 0px; white-space: pre-wrap;"><code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">111 % 3 = 37...0</code> 喝掉<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">111</code>瓶，可以换<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">37</code>瓶汽水, 余<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">0</code>个空瓶</li></ul><ul class="notion-list notion-list-disc notion-block-4bab8101a7b446e19440509231d998b4" style="box-sizing: border-box; margin-block: 0.6em; outline: 0px; margin: 0px; list-style-type: disc; padding-inline-start: 1.7em;"><li style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 6px 0px; white-space: pre-wrap;"><code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">37 % 3 = 12...1</code> 喝掉<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">37</code>瓶，可以换<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">12</code>瓶汽水, 余<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">1</code>个空瓶</li></ul><ul class="notion-list notion-list-disc notion-block-67a00ccdf5554bb8b7288a1f58608de1" style="box-sizing: border-box; margin-block: 0.6em; outline: 0px; margin: 0px; list-style-type: disc; padding-inline-start: 1.7em;"><li style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 6px 0px; white-space: pre-wrap;"><code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">12 % 3 = 4...0</code> 喝掉<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">12</code>瓶，可以换<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">4</code>瓶汽水, 余<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">0</code>个空瓶</li></ul><ul class="notion-list notion-list-disc notion-block-4ec5d648a62b4e3e8afdee217206b208" style="box-sizing: border-box; margin-block: 0.6em; outline: 0px; margin: 0px; list-style-type: disc; padding-inline-start: 1.7em;"><li style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 6px 0px; white-space: pre-wrap;"><code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">4 % 3 = 1...1</code> 喝掉<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">4</code>瓶，可以换<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">1</code>瓶汽水, 余<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">1</code>个空瓶</li></ul><ul class="notion-list notion-list-disc notion-block-3e916ddc66d04f54870886c03e11ecd7" style="box-sizing: border-box; margin-block: 0.6em; outline: 0px; margin: 0px; list-style-type: disc; padding-inline-start: 1.7em;"><li style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 6px 0px; white-space: pre-wrap;">此时剩下<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">1</code>瓶汽水 + <code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">3</code>个空瓶，其中<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">3</code>个空瓶可以再换<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">1</code>瓶</li></ul><ul class="notion-list notion-list-disc notion-block-7c4eb16be7654b78ada109a3180f7a02" style="box-sizing: border-box; margin-block: 0.6em; outline: 0px; margin: 0px; list-style-type: disc; padding-inline-start: 1.7em;"><li style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 6px 0px; white-space: pre-wrap;">此时剩下<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">2</code>瓶，喝掉<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">2</code>瓶，不能再换了。
总共：<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">1000 + 333 + 111 + 37 + 12 + 4 + 2 = 1499</code>瓶</li></ul></div></details>


### **8. 重合问题**

在一天的`**24**`小时之中，时钟的时针、分针和秒针完全重合在一起的时候有几次？都分别是什么时间？

<details class="notion-toggle notion-block-45e2d24742d44f08aeb1e674b04e0475" open="" style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 3px 2px;"><summary style="box-sizing: border-box; margin-block: 0px; outline: none; cursor: pointer; color: var(--theme-color,#42b983); font-weight: 700; font-size: 20px !important;"></summary><div style="box-sizing: border-box; margin-block: 0px; outline: 0px; margin-left: 1.1em;"><ul class="notion-list notion-list-disc notion-block-d2e2a79b0c7947e4999dff0eda7909a3" style="box-sizing: border-box; margin-block: 0.6em; outline: 0px; margin: 0px; list-style-type: disc; padding-inline-start: 1.7em;"><li style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 6px 0px; white-space: pre-wrap;">假设时针的角速度为 <code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">ω（ω = 1 / 120 (度/秒)）</code>，那么分针的角速度就为 <code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">12ω</code>，秒针的角速度为 <code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">720ω</code></li></ul><ul class="notion-list notion-list-disc notion-block-7233d60ad6cd43a89454b4f613a560cc" style="box-sizing: border-box; margin-block: 0.6em; outline: 0px; margin: 0px; list-style-type: disc; padding-inline-start: 1.7em;"><li style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 6px 0px; white-space: pre-wrap;">假设时针和分针在 <code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">t</code> 秒后重合，那么分针在 <code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">t</code> 时间内走过的角度减去时针在 <code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">t</code> 时间内走过的角度，得到的结果肯定是 <code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">360</code> 的整数倍</li></ul><ul class="notion-list notion-list-disc notion-block-d09f78f23c954714b594f699a5681909" style="box-sizing: border-box; margin-block: 0.6em; outline: 0px; margin: 0px; list-style-type: disc; padding-inline-start: 1.7em;"><li style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 6px 0px; white-space: pre-wrap;">根据上面的规则，可以算出<b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">时针和分针</b>重合的时间 – 集合 <code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">A</code></li></ul><ul class="notion-list notion-list-disc notion-block-b0dab35ed60b4e74a86f37e85ac2cdd5" style="box-sizing: border-box; margin-block: 0.6em; outline: 0px; margin: 0px; list-style-type: disc; padding-inline-start: 1.7em;"><li style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 6px 0px; white-space: pre-wrap;">同理也能算出<b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">分针和秒针</b>重合的时间 – 集合 <code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">B</code></li></ul><ul class="notion-list notion-list-disc notion-block-dc8b21830c144236b4e7b8e4c06c149a" style="box-sizing: border-box; margin-block: 0.6em; outline: 0px; margin: 0px; list-style-type: disc; padding-inline-start: 1.7em;"><li style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 6px 0px; white-space: pre-wrap;">那么<b style="box-sizing: border-box; margin-block: 0px; outline: 0px; font-weight: 600;">时针、分针及秒针</b>三者重合的时间就是集合 <code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">A、B</code> 的交集</li></ul><div class="notion-text notion-block-187614cb575e44e3ac9db79a10b16bdc" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">结果：</div><ul class="notion-list notion-list-disc notion-block-8ce52c6d836b4262a44c1349291935ed" style="box-sizing: border-box; margin-block: 0.6em; outline: 0px; margin: 0px; list-style-type: disc; padding-inline-start: 1.7em;"><li style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 6px 0px; white-space: pre-wrap;"><code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">A.length = 22</code></li></ul><ul class="notion-list notion-list-disc notion-block-af4f2b111d734dc19c7efdd1c7d84792" style="box-sizing: border-box; margin-block: 0.6em; outline: 0px; margin: 0px; list-style-type: disc; padding-inline-start: 1.7em;"><li style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 6px 0px; white-space: pre-wrap;"><code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">B.length = 1416</code></li></ul><ul class="notion-list notion-list-disc notion-block-05de586524954a4bb855698c7e0b2faf" style="box-sizing: border-box; margin-block: 0.6em; outline: 0px; margin: 0px; list-style-type: disc; padding-inline-start: 1.7em;"><li style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 6px 0px; white-space: pre-wrap;"><code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">A ∩ B = ['00:00:00', '12:00:00'] = 2</code></li></ul></div></details>

### **9. 赛马问题（腾讯高频）**

- 有`**25**`匹马，每场比赛只能赛`**5**`匹，找最快的`**3**`匹马，至少要赛多少场？

- 有`**64**`匹马，每场比赛只能赛`**8**`匹，找最快的`**4**`匹马，至少要赛多少场？

- 有`**25**`匹马，每场比赛只能赛`**5**`匹，找最快的`**5**`匹马，至少要赛多少场？

<details class="notion-toggle notion-block-0604419444854959a5c7e40db0b77648" open="" style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 3px 2px;"><summary style="box-sizing: border-box; margin-block: 0px; outline: none; cursor: pointer; color: var(--theme-color,#42b983); font-weight: 700; font-size: 20px !important;"></summary><div style="box-sizing: border-box; margin-block: 0px; outline: 0px; margin-left: 1.1em;"><ul class="notion-list notion-list-disc notion-block-26f1990b21424fa29904c3b1934713a9" style="box-sizing: border-box; margin-block: 0.6em; outline: 0px; margin: 0px; list-style-type: disc; padding-inline-start: 1.7em;"><li style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 6px 0px; white-space: pre-wrap;"><code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">25</code>匹马<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">5</code>条跑道找最快的<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">3</code>匹马，需要跑几次？答案：<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">7</code>次</li></ul><ul class="notion-list notion-list-disc notion-block-d75f21044b014893b4fa0a9216788ee8" style="box-sizing: border-box; margin-block: 0.6em; outline: 0px; margin: 0px; list-style-type: disc; padding-inline-start: 1.7em;"><li style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 6px 0px; white-space: pre-wrap;"><code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">64</code>匹马<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">8</code>条跑道找最快的<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">4</code>匹马，需要跑几次？答案：最少<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">10</code>次，最多<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">11</code>次</li></ul><figure class="notion-asset-wrapper notion-asset-wrapper-image notion-block-e61926d37d3e4a01b6ddf6b1e755494b" style="box-sizing: border-box; margin-block: 0px; outline: 0px; margin: 1em 0px; max-width: 100%; min-width: 100%; align-self: center; display: flex; flex-direction: column;"><div style="box-sizing: border-box; margin-block: 0px; outline: 0px; position: relative; display: flex; justify-content: center; align-self: center; width: 754.406px; max-width: 100%; flex-direction: column;"><img src="https://www.notion.so/image/https%3A%2F%2Ftva1.sinaimg.cn%2Flarge%2F0081Kckwly1gls7vtmjw9j324y0kiwzt.jpg?table=block&amp;id=e61926d3-7d3e-4a01-b6dd-f6b1e755494b&amp;cache=v2" loading="lazy" alt="notion image" decoding="async" class="medium-zoom-image" style="box-sizing: border-box; margin-block: 0px; outline: 0px; border-radius: 0px; cursor: zoom-in; transition: transform 0.3s cubic-bezier(0.2, 0, 0.2, 1) 0s !important; width: 754.406px; height: 200.99px; max-height: 100%;"></div></figure><div class="notion-text notion-block-5496b385a5364a9ab7af1b5ef1290e09" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">此时<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">A1</code>显然是第一名，接下来需要找出第<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">2、3、4</code>名</div><figure class="notion-asset-wrapper notion-asset-wrapper-image notion-block-35b387aacdb9423992d5fb17a3f0e6a2" style="box-sizing: border-box; margin-block: 0px; outline: 0px; margin: 1em 0px; max-width: 100%; min-width: 100%; align-self: center; display: flex; flex-direction: column;"><div style="box-sizing: border-box; margin-block: 0px; outline: 0px; position: relative; display: flex; justify-content: center; align-self: center; width: 754.406px; max-width: 100%; flex-direction: column;"><img src="https://www.notion.so/image/https%3A%2F%2Ftva1.sinaimg.cn%2Flarge%2F0081Kckwly1gls84xp950j322k0kgqj9.jpg?table=block&amp;id=35b387aa-cdb9-4239-92d5-fb17a3f0e6a2&amp;cache=v2" loading="lazy" alt="notion image" decoding="async" class="medium-zoom-image" style="box-sizing: border-box; margin-block: 0px; outline: 0px; border-radius: 0px; cursor: zoom-in; transition: transform 0.3s cubic-bezier(0.2, 0, 0.2, 1) 0s !important; width: 754.406px; height: 206.865px; max-height: 100%;"></div></figure><div class="notion-text notion-block-615b48094e97405ca511d6e2d3fb15b2" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">如果<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">A3</code>拿了第一名</div><figure class="notion-asset-wrapper notion-asset-wrapper-image notion-block-0de30bdfb18c4d1b8965acec7cfd6cfd" style="box-sizing: border-box; margin-block: 0px; outline: 0px; margin: 1em 0px; max-width: 100%; min-width: 100%; align-self: center; display: flex; flex-direction: column;"><div style="box-sizing: border-box; margin-block: 0px; outline: 0px; position: relative; display: flex; justify-content: center; align-self: center; width: 754.406px; max-width: 100%; flex-direction: column;"><img src="https://www.notion.so/image/https%3A%2F%2Ftva1.sinaimg.cn%2Flarge%2F0081Kckwly1gls7z4mnnoj326g0k67ov.jpg?table=block&amp;id=0de30bdf-b18c-4d1b-8965-acec7cfd6cfd&amp;cache=v2" loading="lazy" alt="notion image" decoding="async" class="medium-zoom-image" style="box-sizing: border-box; margin-block: 0px; outline: 0px; border-radius: 0px; cursor: zoom-in; transition: transform 0.3s cubic-bezier(0.2, 0, 0.2, 1) 0s !important; width: 754.406px; height: 193.938px; max-height: 100%;"></div></figure><div class="notion-text notion-block-f22fe0501f1541e8bb7a41732730582f" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">如果<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">A3</code>不是第一，也就是说<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">B1</code>拿了第一</div><figure class="notion-asset-wrapper notion-asset-wrapper-image notion-block-a756d260d66d4f33952562813c252d54" style="box-sizing: border-box; margin-block: 0px; outline: 0px; margin: 1em 0px; max-width: 100%; min-width: 100%; align-self: center; display: flex; flex-direction: column;"><div style="box-sizing: border-box; margin-block: 0px; outline: 0px; position: relative; display: flex; justify-content: center; align-self: center; width: 754.406px; max-width: 100%; flex-direction: column;"><img src="https://www.notion.so/image/https%3A%2F%2Ftva1.sinaimg.cn%2Flarge%2F0081Kckwly1gls83sba2uj326y0kwe00.jpg?table=block&amp;id=a756d260-d66d-4f33-9525-62813c252d54&amp;cache=v2" loading="lazy" alt="notion image" decoding="async" class="medium-zoom-image" style="box-sizing: border-box; margin-block: 0px; outline: 0px; border-radius: 0px; cursor: zoom-in; transition: transform 0.3s cubic-bezier(0.2, 0, 0.2, 1) 0s !important; width: 754.406px; height: 199.615px; max-height: 100%;"></div></figure><ul class="notion-list notion-list-disc notion-block-f29bf1b438364173a7e9d2785364eef5" style="box-sizing: border-box; margin-block: 0.6em; outline: 0px; margin: 0px; list-style-type: disc; padding-inline-start: 1.7em;"><li style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 6px 0px; white-space: pre-wrap;"><code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">25</code>匹马<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">5</code>条跑道找最快的<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">5</code>匹马，需要跑几次？答案：最少<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">8</code>次，最多<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">9</code>次</li></ul><figure class="notion-asset-wrapper notion-asset-wrapper-image notion-block-5f54c58fc8784349b3296a15892b922f" style="box-sizing: border-box; margin-block: 0px; outline: 0px; margin: 1em 0px; max-width: 100%; min-width: 100%; align-self: center; display: flex; flex-direction: column;"><div style="box-sizing: border-box; margin-block: 0px; outline: 0px; position: relative; display: flex; justify-content: center; align-self: center; width: 754.406px; max-width: 100%; flex-direction: column;"><img src="https://www.notion.so/image/https%3A%2F%2Ftva1.sinaimg.cn%2Flarge%2F0081Kckwly1gls7v9cethj32420g8n14.jpg?table=block&amp;id=5f54c58f-c878-4349-b329-6a15892b922f&amp;cache=v2" loading="lazy" alt="notion image" decoding="async" class="medium-zoom-image" style="box-sizing: border-box; margin-block: 0px; outline: 0px; border-radius: 0px; cursor: zoom-in; transition: transform 0.3s cubic-bezier(0.2, 0, 0.2, 1) 0s !important; width: 754.406px; height: 160.906px; max-height: 100%;"></div></figure><div class="notion-text notion-block-3ffa757b9b6b4e77b3fb04ab987b735c" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">现在已经跑了<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">5 + 1</code>=<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">6</code>次</div><figure class="notion-asset-wrapper notion-asset-wrapper-image notion-block-4519e4a527e8419d8e6e8056a8f4acb6" style="box-sizing: border-box; margin-block: 0px; outline: 0px; margin: 1em 0px; max-width: 100%; min-width: 100%; align-self: center; display: flex; flex-direction: column;"><div style="box-sizing: border-box; margin-block: 0px; outline: 0px; position: relative; display: flex; justify-content: center; align-self: center; width: 754.406px; max-width: 100%; flex-direction: column;"><img src="https://www.notion.so/image/https%3A%2F%2Ftva1.sinaimg.cn%2Flarge%2F0081Kckwly1gls7oou8h2j324k0g4wun.jpg?table=block&amp;id=4519e4a5-27e8-419d-8e6e-8056a8f4acb6&amp;cache=v2" loading="lazy" alt="notion image" decoding="async" class="medium-zoom-image" style="box-sizing: border-box; margin-block: 0px; outline: 0px; border-radius: 0px; cursor: zoom-in; transition: transform 0.3s cubic-bezier(0.2, 0, 0.2, 1) 0s !important; width: 754.406px; height: 158.76px; max-height: 100%;"></div></figure><div class="notion-text notion-block-0f7c67dc4cf64d05b7cd6188c5c8e92e" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">现在已经跑了<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">5 + 1 + 1</code> = <code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">7</code>次</div><figure class="notion-asset-wrapper notion-asset-wrapper-image notion-block-51b2e861b3db4eddb5432bde46e15803" style="box-sizing: border-box; margin-block: 0px; outline: 0px; margin: 1em 0px; max-width: 100%; min-width: 100%; align-self: center; display: flex; flex-direction: column;"><div style="box-sizing: border-box; margin-block: 0px; outline: 0px; position: relative; display: flex; justify-content: center; align-self: center; width: 754.406px; max-width: 100%; flex-direction: column;"><img src="https://www.notion.so/image/https%3A%2F%2Ftva1.sinaimg.cn%2Flarge%2F0081Kckwly1gls7ok26wbj31ki0u01kx.jpg?table=block&amp;id=51b2e861-b3db-4edd-b543-2bde46e15803&amp;cache=v2" loading="lazy" alt="notion image" decoding="async" class="medium-zoom-image" style="box-sizing: border-box; margin-block: 0px; outline: 0px; border-radius: 0px; cursor: zoom-in; transition: transform 0.3s cubic-bezier(0.2, 0, 0.2, 1) 0s !important; width: 754.406px; height: 400.562px; max-height: 100%;"></div></figure></div></details>

 

### **10. 烧香确定时间问题**

有两根不均匀的香，燃烧完都需要一个小时，问怎么确定`**15**`分钟的时长？

<details class="notion-toggle notion-block-cb07f82aa6a94d868e60ae500215f6ba" open="" style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 3px 2px;"><summary style="box-sizing: border-box; margin-block: 0px; outline: none; cursor: pointer; color: var(--theme-color,#42b983); font-weight: 700; font-size: 20px !important;"></summary><div style="box-sizing: border-box; margin-block: 0px; outline: 0px; margin-left: 1.1em;"><div class="notion-text notion-block-5151c7694fb148e88fb9024a3f872322" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 2px 0px 1px;">相对时间的思路。</div><div class="notion-text notion-block-4f63211df93b4d409c9bf1beaef5157f" style="box-sizing: border-box; margin-block: 0px; outline: 0px; width: 754.406px; white-space: pre-wrap; word-break: break-word; padding: 0.5em 2px; margin: 1px 0px;">答：设两根香分别为<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">A</code>、<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">B</code>，先把<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">A</code>一端点燃，然后把<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">B</code>的两端都点燃，这样当<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">B</code>烧完的时候，<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">A</code>就还剩下一半（此时能确定半小时），此时把<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">A</code>的另一端也点燃，那么从此刻到<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">A</code>烧完的时间就是<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">15</code>分钟。</div></div></details>

### **11. 掰巧克力问题**

- `**N\*M**`块巧克力，每次掰一块的一行或一列，掰成`**1\*1**`的巧克力需要多少次？

- 淘汰问题：`**1000**`个人参加辩论赛，`**1V1**`，输了就退出，需要安排多少场比赛？

<details class="notion-toggle notion-block-d316cb3e17df4ef5b893c8cbceecfe8a" open="" style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 3px 2px;"><summary style="box-sizing: border-box; margin-block: 0px; outline: none; cursor: pointer; color: var(--theme-color,#42b983); font-weight: 700; font-size: 20px !important;"></summary><div style="box-sizing: border-box; margin-block: 0px; outline: 0px; margin-left: 1.1em;"><ul class="notion-list notion-list-disc notion-block-4a1e12fac6fd444b99d4dac55bbc89c2" style="box-sizing: border-box; margin-block: 0.6em; outline: 0px; margin: 0px; list-style-type: disc; padding-inline-start: 1.7em;"><li style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 6px 0px; white-space: pre-wrap;">每次拿起一块巧克力，掰一下（无论横着还是竖着）都会变成两块，因为所有的巧克力共有<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">N*M</code>块，所以要掰<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">N*M-1</code>次，减<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">1</code>是因为最开始的一块是不用算进去的。</li></ul><ul class="notion-list notion-list-disc notion-block-711c2fcd7981497b93e37d1301d5bc2a" style="box-sizing: border-box; margin-block: 0.6em; outline: 0px; margin: 0px; list-style-type: disc; padding-inline-start: 1.7em;"><li style="box-sizing: border-box; margin-block: 0px; outline: 0px; padding: 6px 0px; white-space: pre-wrap;">每一场辩论赛两个人，淘汰一个人，所以可以看作是每一场辩论赛减少一个人，直到最后剩下<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">1</code>个人，所以是<code class="notion-inline-code" style="box-sizing: border-box; margin-block: 0px; outline: 0px; color: rgb(255, 64, 129); padding: 0.2em 0.4em !important; background: rgba(55, 53, 47, 0.1) !important; border-radius: 3px; font-size: 13.6px; font-family: SFMono-Regular, Consolas, &quot;Liberation Mono&quot;, Menlo, Courier, monospace; border: 0px !important; box-shadow: none !important;">1000 - 1 = 999</code>场。</li></ul></div></details>



## 常考题

不管是春招还是秋招，校招生是避免不了刷题操作的，今天我总结了一下自己秋招过程对leetcode题目进行分类并针对性练习的过程。  

一些基本的数据结构练习，建议结合大话数据结构这本书食用。里面有一部分语言特性，注意总结与分析，有助于加深数据结构基础的理解。  
**基本数据结构总结**  
推荐题目：

*   [LeetCode 1. Two Sum](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Ftwo-sum%2F "https://leetcode-cn.com/problems/two-sum/")
*   [LeetCode 187. Repeated DNA Sequences](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Frepeated-dna-sequences%2F "https://leetcode-cn.com/problems/repeated-dna-sequences/")
*   [LeetCode 706. Design HashMap](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fdesign-hashmap%2F "https://leetcode-cn.com/problems/design-hashmap/")
*   [LeetCode 652. Find Duplicate Subtrees](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Ffind-duplicate-subtrees%2F "https://leetcode-cn.com/problems/find-duplicate-subtrees/")
*   [LeetCode 560. Subarray Sum Equals K](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fsubarray-sum-equals-k%2F "https://leetcode-cn.com/problems/subarray-sum-equals-k/")
*   [LeetCode 547. Friend Circles](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Ffriend-circles%2F "https://leetcode-cn.com/problems/friend-circles/")
*   [LeetCode 684. Redundant Connection](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fredundant-connection%2F "https://leetcode-cn.com/problems/redundant-connection/")
*   [LeetCode 692. Top K Frequent Words](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Ftop-k-frequent-words%2F "https://leetcode-cn.com/problems/top-k-frequent-words/")
*   [LeetCode 295. Find Median from Data Stream](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Ffind-median-from-data-stream%2F "https://leetcode-cn.com/problems/find-median-from-data-stream/")
*   [LeetCode 352. Data Stream as Disjoint Intervals](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fdata-stream-as-disjoint-intervals%2F "https://leetcode-cn.com/problems/data-stream-as-disjoint-intervals/")


二分查找一般是在单调有序的数组上操作，而实际的变体却是很灵活的。例如lc287题就是一种经典的应用，关于二分内容，推荐下面几道题目，扣好边界是关键。  
**二分专题**

*   [Leetcode 69. sqrt x](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fsqrtx%2F "https://leetcode-cn.com/problems/sqrtx/")
*   [Leetcode 35. Search insert position](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fsearch-insert-position%2F "https://leetcode-cn.com/problems/search-insert-position/")
*   [LeetCode 34. Find First and Last Position of Element in Sorted Array](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Ffind-first-and-last-position-of-element-in-sorted-array%2F "https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/")
*   [LeetCode 74. Search a 2D Matrix](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fsearch-a-2d-matrix%2F "https://leetcode-cn.com/problems/search-a-2d-matrix/")
*   [LeetCode 153. Find Minimum in Rotated Sorted Array](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Ffind-minimum-in-rotated-sorted-array%2F "https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array/")
*   [LeetCode 33. Search in Rotated Sorted Array](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fsearch-in-rotated-sorted-array%2F "https://leetcode-cn.com/problems/search-in-rotated-sorted-array/")
*   [LeetCode 278. First Bad Version](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Ffirst-bad-version%2F "https://leetcode-cn.com/problems/first-bad-version/")
*   [LeetCode 162. Find Peak Element](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Ffind-peak-element%2F "https://leetcode-cn.com/problems/find-peak-element/")
*   [LeetCode 287. Find the Duplicate Number](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Ffind-the-duplicate-number%2F "https://leetcode-cn.com/problems/find-the-duplicate-number/")
*   [LeetCode 275. H-Index II](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fh-index-ii%2F "https://leetcode-cn.com/problems/h-index-ii/")


关于链表，考点居多，但是常考的题目固定，校招过程中，遇到的更多的是逆置等问题，这里总结了几道题目，个人建议将链表排序这部分着重复习，例如链表快排，链表插排，链表归并排，都考过，尤其是字节的面试官，非常喜欢考链表的题目，这部分题目，扣好细节即可。  
**链表专题**  
推荐题目:

*   [LeetCode 19. Remove Nth Node From End of List](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fremove-nth-node-from-end-of-list%2F "https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/")
*   [LeetCode 237. Delete Node in a Linked List](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fdelete-node-in-a-linked-list%2F "https://leetcode-cn.com/problems/delete-node-in-a-linked-list/")
*   [LeetCode 83. Remove Duplicates from Sorted List](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fremove-duplicates-from-sorted-list%2F "https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list/")
*   [LeetCode 61. Rotate List](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Frotate-list%2F "https://leetcode-cn.com/problems/rotate-list/")
*   [LeetCode 24. Swap Nodes in Pairs](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fswap-nodes-in-pairs%2F "https://leetcode-cn.com/problems/swap-nodes-in-pairs/")
*   [LeetCode 206. Reverse Linked List](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Freverse-linked-list%2F "https://leetcode-cn.com/problems/reverse-linked-list/")
*   [LeetCode 92. Reverse Linked List II](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Freverse-linked-list-ii%2F "https://leetcode-cn.com/problems/reverse-linked-list-ii/")
*   [LeetCode 160. Intersection of Two Linked Lists](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fintersection-of-two-linked-lists%2F "https://leetcode-cn.com/problems/intersection-of-two-linked-lists/")
*   [LeetCode 142. Linked List Cycle II](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Flinked-list-cycle-ii%2F "https://leetcode-cn.com/problems/linked-list-cycle-ii/")
*   [LeetCode 148. Sort List](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fsort-list%2F "https://leetcode-cn.com/problems/sort-list/")

树与二叉树同样是字节面试官喜欢考的内容，因为这一部分内容能够很好的验证面试者对递归操作得理解与掌握。内容以二叉树居多，二叉树的几种遍历方法需要烂熟于心（非递归版本）  
**树专题**  
推荐题目:

*   [LeetCode 98. Validate Binary Search Tree](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fvalidate-binary-search-tree%2F "https://leetcode-cn.com/problems/validate-binary-search-tree/")
*   [LeetCode 101. Symmetric Tree](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fsymmetric-tree%2F "https://leetcode-cn.com/problems/symmetric-tree/")
*   [LeetCode 94. Binary Tree Inorder Traversal](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fbinary-tree-inorder-traversal%2F "https://leetcode-cn.com/problems/binary-tree-inorder-traversal/")
*   [LeetCode 105. Construct Binary Tree from Preorder and Inorder Traversal](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fconstruct-binary-tree-from-preorder-and-inorder-traversal%2F "https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/")
*   [LeetCode 102. Binary Tree Level Order Traversal](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fbinary-tree-level-order-traversal%2F "https://leetcode-cn.com/problems/binary-tree-level-order-traversal/")
*   [LeetCode 236. Lowest Common Ancestor of a Binary Tree](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Flowest-common-ancestor-of-a-binary-tree%2F "https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree/")
*   [LeetCode 297. Serialize and Deserialize Binary Tree](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fserialize-and-deserialize-binary-tree%2F "https://leetcode-cn.com/problems/serialize-and-deserialize-binary-tree/")
*   [LeetCode 543. Diameter of Binary Tree](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fdiameter-of-binary-tree%2F "https://leetcode-cn.com/problems/diameter-of-binary-tree/")
*   [LeetCode 124. Binary Tree Maximum Path Sum](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fbinary-tree-maximum-path-sum%2F "https://leetcode-cn.com/problems/binary-tree-maximum-path-sum/")
*   [LeetCode 173. Binary Search Tree Iterator](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fbinary-search-tree-iterator%2F "https://leetcode-cn.com/problems/binary-search-tree-iterator/")

字符串处理是常见题目，这部分不多说，主要空格和逗号，属于一些常规题目，简单推荐几道，可以包含几种常见的类型了  
**字符串处理**  
推荐题目:

*   [LeetCode 38. Count and Say](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fcount-and-say%2F "https://leetcode-cn.com/problems/count-and-say/")
*   [LeetCode 49. Group Anagrams](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fgroup-anagrams%2F "https://leetcode-cn.com/problems/group-anagrams/")
*   [LeetCode 151. Reverse Words in a String](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Freverse-words-in-a-string%2F "https://leetcode-cn.com/problems/reverse-words-in-a-string/")
*   [LeetCode 165. Compare Version Numbers](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fcompare-version-numbers%2F "https://leetcode-cn.com/problems/compare-version-numbers/")
*   [LeetCode 929. Unique Email Addresses](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Funique-email-addresses%2F "https://leetcode-cn.com/problems/unique-email-addresses/")
*   [LeetCode 5. Longest Palindromic Substring](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Flongest-palindromic-substring%2F "https://leetcode-cn.com/problems/longest-palindromic-substring/")
*   [LeetCode 6. ZigZag Conversion](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fzigzag-conversion%2F "https://leetcode-cn.com/problems/zigzag-conversion/")
*   [LeetCode 3. Longest Substring Without Repeating Characters](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Flongest-substring-without-repeating-characters%2F "https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/")
*   [LeetCode 208. Implement Trie (Prefix Tree)](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fimplement-trie-prefix-tree%2F "https://leetcode-cn.com/problems/implement-trie-prefix-tree/")
*   [LeetCode 273. Integer to English Words](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Finteger-to-english-words%2F "https://leetcode-cn.com/problems/integer-to-english-words/")

从这开始，进入虐心模式，这部分题目我刷了整整两天，刷的清爽的不得了。主要是深度优先搜索与回溯，这部分时间复杂度较大，经常难以找到合适的思路。  
**回溯法与深度优先搜索**  
推荐题目：

*   [LeetCode 17. Letter Combinations of a Phone Number](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fletter-combinations-of-a-phone-number%2F "https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number/")
*   [LeetCode 79. Word Search](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fword-search%2F "https://leetcode-cn.com/problems/word-search/")
*   [LeetCode 46. Permutations](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fpermutations%2F "https://leetcode-cn.com/problems/permutations/")
*   [LeetCode 47. Permutations II](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fpermutations-ii%2F "https://leetcode-cn.com/problems/permutations-ii/")
*   [LeetCode 78. Subsets](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fsubsets%2F "https://leetcode-cn.com/problems/subsets/")
*   [LeetCode 90. Subsets II](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fsubsets-ii%2F "https://leetcode-cn.com/problems/subsets-ii/")
*   [LeetCode 216. Combination Sum III](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fcombination-sum-iii%2F "https://leetcode-cn.com/problems/combination-sum-iii/")
*   [LeetCode 52. N-Queens II](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fn-queens-ii%2F "https://leetcode-cn.com/problems/n-queens-ii/")
*   [LeetCode 37. Sudoku Solver](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fsudoku-solver%2F "https://leetcode-cn.com/problems/sudoku-solver/")
*   [LeetCode 473. Matchsticks to Square](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fmatchsticks-to-square%2F "https://leetcode-cn.com/problems/matchsticks-to-square/")

这部分题目涉及到一些较为复杂的数据结构，  
**滑动窗口、双指针与单调队列/栈**  
推荐题目：

*   [LeetCode 167. Two Sum II - Input array is sorted](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Ftwo-sum-ii-input-array-is-sorted%2F "https://leetcode-cn.com/problems/two-sum-ii-input-array-is-sorted/")
*   [LeetCode 88. Merge Sorted Array](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fmerge-sorted-array%2F "https://leetcode-cn.com/problems/merge-sorted-array/")
*   [LeetCode 26. Remove Duplicates from Sorted Array](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fremove-duplicates-from-sorted-array%2F "https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/")
*   [LeetCode 76. Minimum Window Substring](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fminimum-window-substring%2F "https://leetcode-cn.com/problems/minimum-window-substring/")
*   [LeetCode 32. Longest Valid Parentheses](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Flongest-valid-parentheses%2F "https://leetcode-cn.com/problems/longest-valid-parentheses/")
*   [LeetCode 155. Min Stack](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fmin-stack%2F "https://leetcode-cn.com/problems/min-stack/")
*   [LeetCode 42. Trapping Rain Water](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Ftrapping-rain-water%2F "https://leetcode-cn.com/problems/trapping-rain-water/")
*   [LeetCode 84. Largest Rectangle in Histogram](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Flargest-rectangle-in-histogram%2F "https://leetcode-cn.com/problems/largest-rectangle-in-histogram/")
*   [LeetCode 239. Sliding Window Maximum](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fsliding-window-maximum%2F "https://leetcode-cn.com/problems/sliding-window-maximum/")
*   [LeetCode 918. Maximum Sum Circular Subarray](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fmaximum-sum-circular-subarray%2F "https://leetcode-cn.com/problems/maximum-sum-circular-subarray/")


对于我来说，最难的部分，但是学会之后就会很舒服。DP日渐成为各大公司面试的必考点。通过DP可以有效的减少时间复杂度与重复计算。  
**动态规划**  
推荐题目：

*   [LeetCode 53. Maximum Subarray](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fmaximum-subarray%2F "https://leetcode-cn.com/problems/maximum-subarray/")
*   [LeetCode 120. Triangle](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Ftriangle%2F "https://leetcode-cn.com/problems/triangle/")
*   [LeetCode 63. Unique Paths II](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Funique-paths-ii%2F "https://leetcode-cn.com/problems/unique-paths-ii/")
*   [LeetCode 91. Decode Ways](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fdecode-ways%2F "https://leetcode-cn.com/problems/decode-ways/")
*   [LeetCode 198. House Robber](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fhouse-robber%2F "https://leetcode-cn.com/problems/house-robber/") 
*   [LeetCode 300. Longest Increasing Subsequence](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Flongest-increasing-subsequence%2F "https://leetcode-cn.com/problems/longest-increasing-subsequence/")
*   [LeetCode 72. Edit Distance](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fedit-distance%2F "https://leetcode-cn.com/problems/edit-distance/")
*   [LeetCode 518. Coin Change 2](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fcoin-change-2%2F "https://leetcode-cn.com/problems/coin-change-2/")
*   [LeetCode 664. Strange Printer](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fstrange-printer%2F "https://leetcode-cn.com/problems/strange-printer/")
*   [LeetCode 10. Regular Expression Matching](https://link.juejin.cn/?target=https%3A%2F%2Fleetcode-cn.com%2Fproblems%2Fregular-expression-matching%2F "https://leetcode-cn.com/problems/regular-expression-matching/")

以上，是我刷的部分leetcode题目，偶尔还会打打周赛。另外，剑指offer是必刷的。个人比较推荐牛客网的剑指offer题目。最后，祝各位同学面试顺利，拿到满意的offer  

#### **二分查找**

- [**二分查找**](https://www.nowcoder.com/practice/7bc4a1c7c371425d9faa9d1b511fe193?tpId=190&&tqId=35227&rp=1&ru=/ta/job-code-high-rd&qru=/ta/job-code-high-rd/question-ranking)[牛客]：LC上找不到一模一样的。

- [**求平方根**](https://leetcode-cn.com/problems/sqrtx/)

#### **滑动窗口**

- [**滑动窗口的最大值**](https://leetcode-cn.com/problems/hua-dong-chuang-kou-de-zui-da-zhi-lcof/)

- [**滑动窗口的中位数**](https://leetcode-cn.com/problems/sliding-window-median/)

- [**最长不含重复字符的子字符串**](https://leetcode-cn.com/problems/zui-chang-bu-han-zhong-fu-zi-fu-de-zi-zi-fu-chuan-lcof/)

#### **数组**

- [**合并两个有序数组**](https://leetcode-cn.com/problems/merge-sorted-array/)

- [**数组中出现超过一半的数\***](https://leetcode-cn.com/problems/shu-zu-zhong-chu-xian-ci-shu-chao-guo-yi-ban-de-shu-zi-lcof/)

- [**岛屿的最大面积**](https://leetcode-cn.com/problems/max-area-of-island/)

- [**接雨水**](https://leetcode-cn.com/problems/trapping-rain-water/)

- [**螺旋矩阵**](https://leetcode-cn.com/problems/spiral-matrix/)

- [**逆序对\***](https://leetcode-cn.com/problems/shu-zu-zhong-de-ni-xu-dui-lcof/)

#### **链表**

- [**反转链表**](https://leetcode-cn.com/problems/reverse-linked-list/)

- [**k个一组反转链表**](https://leetcode-cn.com/problems/reverse-nodes-in-k-group/)

- [**删除排序链表中的重复元素**](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list/)

- [**环形链表**](https://leetcode-cn.com/problems/linked-list-cycle/)

- [**两个链表的第一个公共节点**](https://leetcode-cn.com/problems/liang-ge-lian-biao-de-di-yi-ge-gong-gong-jie-dian-lcof/)

- [**合并有序链表**](https://leetcode-cn.com/problems/he-bing-liang-ge-pai-xu-de-lian-biao-lcof/)

- [**链表求和**](https://leetcode-cn.com/problems/sum-lists-lcci/)

- [**回文链表**](https://leetcode-cn.com/problems/palindrome-linked-list/)

- [**复制带随机指针的链表**](https://leetcode-cn.com/problems/copy-list-with-random-pointer/)

#### **二叉树**

- [**二叉树的深度**](https://leetcode-cn.com/problems/er-cha-shu-de-shen-du-lcof/)

- [**之字形打印二叉树**](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/)

- [**二叉搜索树的第 k 大节点**](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-di-kda-jie-dian-lcof/)

- [**二叉树的最近公共祖先**](https://leetcode-cn.com/problems/er-cha-shu-de-zui-jin-gong-gong-zu-xian-lcof/)

- [**二叉树中和为某一值的路径\***](https://leetcode-cn.com/problems/er-cha-shu-zhong-he-wei-mou-yi-zhi-de-lu-jing-lcof/)

- [**二叉树的最大路径和**](https://leetcode-cn.com/problems/binary-tree-maximum-path-sum/)

- [**二叉树的右视图\***](https://leetcode-cn.com/problems/binary-tree-right-side-view/)

#### **TopK**

- [**最小的k个数**](https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/)

- [**数组中的第K个最大元素**](https://leetcode-cn.com/problems/kth-largest-element-in-an-array/)

#### **设计题**

- [**最小栈**](https://leetcode-cn.com/problems/min-stack/)

- [**两个栈实现队列**](https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/)

- [**LRU缓存机制**](https://leetcode-cn.com/problems/lru-cache/)

#### **动态规划**

- [**青蛙跳台阶**](https://leetcode-cn.com/problems/qing-wa-tiao-tai-jie-wen-ti-lcof/)

- [**最长上升子序列**](https://leetcode-cn.com/problems/longest-increasing-subsequence/)

- [**最长公共子序列**](https://leetcode-cn.com/problems/longest-common-subsequence/)

- [**编辑距离\***](https://leetcode-cn.com/problems/edit-distance/)

- [**零钱兑换2\***](https://leetcode-cn.com/problems/coin-change-2/)

#### **其他**

- [**翻转单词顺序**](https://leetcode-cn.com/problems/fan-zhuan-dan-ci-shun-xu-lcof/)

- [**二进制中1的个数\***](https://leetcode-cn.com/problems/er-jin-zhi-zhong-1de-ge-shu-lcof/)

- [**颠倒二进制位\***](https://leetcode-cn.com/problems/reverse-bits/)

- [**数据流中的中位数\***](https://leetcode-cn.com/problems/shu-ju-liu-zhong-de-zhong-wei-shu-lcof/)

- [**复原IP地址**](https://leetcode-cn.com/problems/restore-ip-addresses/)

#### **系列题**

#### **X数之和系列：**

- [**两数之和**](https://leetcode-cn.com/problems/two-sum/)

- [**三数之和**](https://leetcode-cn.com/problems/3sum/)

- [**最接近的三数之和\***](https://leetcode-cn.com/problems/3sum-closest/)

#### **股票系列：**

> 这系列还有4，有余力的同学可以做做

- [**买卖股票的最佳时机1**](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/)

- [**买卖股票的最佳时机2**](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/)

- [**买卖股票的最佳时机3**](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-iii/)

#### **括号系列：**

> 注意解法上的优化，这系列要搞定最优解

- [**有效括号**](https://leetcode-cn.com/problems/valid-parentheses/)

- [**最长有效括号**](https://leetcode-cn.com/problems/longest-valid-parentheses/)

### **各公司常考题补充**

> 下方列表，展示的是除了上面提到的题目以外，各自还常考的题目。

#### **字节（待验证）**

- [**单词搜索**](https://leetcode-cn.com/problems/word-search/)

- [**重排链表**](https://leetcode-cn.com/problems/reorder-list/)

- [**验证栈序列**](https://leetcode-cn.com/problems/validate-stack-sequences/)

- [**字典序排数**](https://leetcode-cn.com/problems/lexicographical-numbers/)

- [**寻找两个正序数组的中位数**](https://leetcode-cn.com/problems/median-of-two-sorted-arrays/)

- [**剪绳子I**](https://leetcode-cn.com/problems/jian-sheng-zi-lcof/)

- [**剪绳子II**](https://leetcode-cn.com/problems/jian-sheng-zi-ii-lcof/)

- [**最长回文子串**](https://leetcode-cn.com/problems/longest-palindromic-substring/)

- [**下一个数**](https://leetcode-cn.com/problems/closed-number-lcci/)
