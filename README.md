# 排序報告

學號: 11428124  
姓名: 尤柏鈞  
模擬頁面: [https://github.com/kk5566123/sort_report](https://github.com/kk5566123/sort_report)

## 氣泡排序法
#### 1. 簡述原理

氣泡排序法是一種簡單且直觀的排序演算法。它的運作原理是重複地走訪要排序的數列，每次比較相鄰的兩個元素。如果這兩個元素的順序錯誤（例如：要求由小到大排序，但前面的元素大於後面的元素），就將它們交換位置。
走訪數列的工作會重複進行，直到在一整個迴圈中都沒有發生任何交換，這就代表該數列已經排序完成。這個演算法的名字由來，是因為數列中較大（或較小）的元素會透過一次次的交換，如同水中的氣泡一樣慢慢「浮」到數列的頂端（或尾端）。

#### 2. 複雜度分析

* **時間複雜度 (Time Complexity):**
    * **最佳情況 (Best Case):** $O(n)$。當輸入的數列已經是完全排序好的狀態，加上提早結束的優化機制（檢查是否發生交換），只需要走訪數列一次即可完成。
    * **最壞情況 (Worst Case):** $O(n^2)$。當輸入的數列是完全反向排序時，每一圈都需要進行最大次數的比較與交換。
    * **平均情況 (Average Case):** $O(n^2)$。
* **空間複雜度 (Space Complexity):**
    * $O(1)$。氣泡排序法只需要常數個額外的記憶體空間（用來暫存交換用的變數），因此屬於**原地排序 (In-place sort)**。
* **穩定性 (Stability):** * **穩定 (Stable)**。在比較相鄰元素時，只有在大於（或小於）的情況下才會交換，如果兩個元素相等則不會交換，因此相同大小的元素在排序後的相對位置不會改變。
  #### 3. 模擬實作內容與執行時間分析

為了測試氣泡排序法在不同資料量下的實際效能，我們實作了氣泡排序法，並引入 `<time.h>` 函式庫中的 `clock()` 來測量程式執行的時間。程式會隨機生成指定數量的整數陣列，並計算排序該陣列所需的花費時間。

**C 語言實作程式碼：**
```c
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>
#include <time.h>

void bubbleSort(int arr[], int n) {
    int i, j, temp;
    bool swapped;
    
    for (i = 0; i < n - 1; i++) {
        swapped = false;
        for (j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
                swapped = true;
            }
        }
        if (swapped == false) {
            break;
        }
    }
}

int main() {
    int n = 10000; // 可更改此數值測試不同資料量
    int *arr = (int*)malloc(n * sizeof(int));
    
    // 產生隨機亂數資料
    for(int i = 0; i < n; i++) {
        arr[i] = rand() % 100000; 
    }

    // 記錄開始時間
    clock_t start_time = clock();
    
    // 執行氣泡排序
    bubbleSort(arr, n);
    
    // 記錄結束時間
    clock_t end_time = clock();
    
    // 計算執行時間 (秒)
    double time_spent = (double)(end_time - start_time) / CLOCKS_PER_SEC;
    printf("資料數量: %d, 執行時間: %f 秒\n", n, time_spent);
    
    free(arr);
    return 0;
}
```
**執行時間測試結果：**

| 資料數量 ($n$) | 執行時間 (秒) | 觀察與分析 |
| :---: | :---: | :--- |
| 1,000 | 0.1476 | 資料量小時，處理速度極快。 |
| 5,000 | 3.2468 | 資料量增加 5 倍，時間增加約 20 倍。 |
| 10,000 | 15.1364 | 資料量增加 10 倍，時間增加超過 100 倍。 |
| 20,000 | 59.9451 | 隨著數量持續增加，時間呈現明顯的平方級數暴增，符合 $O(n^2)$ 特性。 |

## 選擇排序法
#### 1. 簡述原理

選擇排序法的概念非常直觀。它將數列分為「已排序」與「未排序」兩個部分。一開始，已排序部分是空的，所有的元素都在未排序部分。
演算法的運作方式是：在未排序的數列中，尋找最小值（或最大值），然後將這個最小值與未排序部分的第一個元素交換位置。交換完成後，該元素就被納入「已排序」部分。接著，對剩下的未排序元素重複這個尋找與交換的動作，直到所有的元素都完成排序。

#### 2. 複雜度分析

* **時間複雜度 (Time Complexity):**
    * **最佳情況 (Best Case):** $O(n^2)$。即使輸入的數列已經是完全排序好的狀態，選擇排序法仍然需要走訪未排序部分來「確認」它是最小值，因此無論如何都需要進行相同次數的比較。
    * **最壞情況 (Worst Case):** $O(n^2)$。
    * **平均情況 (Average Case):** $O(n^2)$。
* **空間複雜度 (Space Complexity):**
    * $O(1)$。選擇排序法只需要常數個額外的記憶體空間來記錄最小值的索引和進行交換，屬於**原地排序 (In-place sort)**。
* **穩定性 (Stability):** * **不穩定 (Unstable)**。在交換的過程中，可能會破壞相同大小元素的原本相對順序。例如數列 `[4(a), 4(b), 1]`，第一步會將 `1` 和 `4(a)` 交換，變成 `[1, 4(b), 4(a)]`，此時兩個 `4` 的相對位置就改變了。

#### 3. 模擬實作內容與執行時間分析

為了測試選擇排序法的效能，我們同樣使用 C 語言進行實作，並利用 `<time.h>` 測量不同資料量下的執行時間。

**C 語言實作程式碼：**
```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

void selectionSort(int arr[], int n) {
    int i, j, min_idx, temp;
    
    // 逐步移動未排序部分的邊界
    for (i = 0; i < n - 1; i++) {
        // 假設未排序部分的第一個元素是最小值
        min_idx = i;
        
        // 在剩下的元素中尋找實際的最小值
        for (j = i + 1; j < n; j++) {
            if (arr[j] < arr[min_idx]) {
                min_idx = j; // 更新最小值所在的索引
            }
        }
        
        // 將找到的最小值與未排序部分的第一個元素交換
        if (min_idx != i) {
            temp = arr[i];
            arr[i] = arr[min_idx];
            arr[min_idx] = temp;
        }
    }
}

int main() {
    int n = 10000; // 可更改此數值測試不同資料量
    int *arr = (int*)malloc(n * sizeof(int));
    
    // 產生隨機亂數資料
    for(int i = 0; i < n; i++) {
        arr[i] = rand() % 100000; 
    }

    // 記錄開始時間
    clock_t start_time = clock();
    
    // 執行選擇排序
    selectionSort(arr, n);
    
    // 記錄結束時間
    clock_t end_time = clock();
    
    // 計算執行時間 (秒)
    double time_spent = (double)(end_time - start_time) / CLOCKS_PER_SEC;
    printf("資料數量: %d, 執行時間: %f 秒\n", n, time_spent);
    
    free(arr);
    return 0;
}
```
### 選擇排序法執行時間測試結果

下表為不同隨機資料數量 ($n$) 在選擇排序法下的執行時間測試結果。

| 資料數量 ($n$) | 執行時間 (秒) | 觀察與分析 |
| :---: | :---: | :--- |
| 1,000 | 0.0535 | 執行速度極快。 |
| 5,000 | 1.3589 | 資料量增加 5 倍，時間增加超過 20 倍。 |
| 10,000 | 5.3728 | 相比於氣泡排序，選擇排序的交換次數較少，因此在實際執行時間上通常會比氣泡排序快一些，但成長趨勢依舊。 |
| 20,000 | 22.6301 | 當資料量翻倍為 20,000 時，時間約為 10,000 筆時的 4 倍，完全符合 $O(n^2)$ 的時間複雜度曲線。 |

## 插入排序法
#### 1. 簡述原理

插入排序法的原理非常貼近我們日常生活中玩撲克牌時「整理手牌」的動作。演算法會將數列分為「已排序」與「未排序」兩個部分。一開始，假設數列的第一個元素已經排序好。

接下來，從未排序部分的第二個元素開始，每次取出一個元素（稱為 Key），將其與已排序部分的元素由後往前逐一比較。如果已排序的元素大於 Key，就將該元素往後移一格，直到找到一個小於或等於 Key 的元素，或是已經比對到數列最前端，再將 Key 插入到該位置。



#### 2. 複雜度分析

* **時間複雜度 (Time Complexity):**
    * **最佳情況 (Best Case):** $O(n)$。當輸入的數列已經是完全排序好的狀態，每次取出的元素只需要跟前一個元素比較一次，不需要進行任何移動即可確認位置。
    * **最壞情況 (Worst Case):** $O(n^2)$。當輸入的數列是完全反向排序時，每次取出的元素都需要與前面所有已排序的元素進行比較並移動。
    * **平均情況 (Average Case):** $O(n^2)$。
* **空間複雜度 (Space Complexity):**
    * $O(1)$。插入排序法只需要常數個額外的記憶體空間來存放 Key 變數，屬於**原地排序 (In-place sort)**。
* **穩定性 (Stability):** * **穩定 (Stable)**。在比較與移動的過程中，只有遇到嚴格大於 Key 的元素才會將其後移，若遇到相等的元素，Key 會插在其後方，因此相同大小元素的相對位置不會改變。

#### 3. 模擬實作內容與執行時間分析

同樣使用 C 語言進行實作，並利用 `<time.h>` 測量不同資料量下的執行時間。

**C 語言實作程式碼：**
```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

void insertionSort(int arr[], int n) {
    int i, key, j;
    
    // 從陣列的第二個元素開始，假設第一個元素(索引0)已排序
    for (i = 1; i < n; i++) {
        key = arr[i]; // 取出未排序部分的第一個元素作為 key
        j = i - 1;
        
        // 將 key 與已排序部分的元素由後往前比較
        // 如果已排序元素大於 key，則將其往後移動一格
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        
        // 將 key 插入到正確的位置
        arr[j + 1] = key;
    }
}

int main() {
    int n = 10000; // 可更改此數值測試不同資料量
    int *arr = (int*)malloc(n * sizeof(int));
    
    // 產生隨機亂數資料
    for(int i = 0; i < n; i++) {
        arr[i] = rand() % 100000; 
    }

    // 記錄開始時間
    clock_t start_time = clock();
    
    // 執行插入排序
    insertionSort(arr, n);
    
    // 記錄結束時間
    clock_t end_time = clock();
    
    // 計算執行時間 (秒)
    double time_spent = (double)(end_time - start_time) / CLOCKS_PER_SEC;
    printf("資料數量: %d, 執行時間: %f 秒\n", n, time_spent);
    
    free(arr);
    return 0;
}
```
**執行時間測試結果：**

| 資料數量 ($n$) | 執行時間 (秒) | 觀察與分析 |
| :---: | :---: | :--- |
| 10,000 | 0.0018 | 相比於前幾種 $O(n^2)$ 演算法，合併排序在此資料量下的時間幾乎可以忽略不計。 |
| 20,000 | 0.0039 | 資料量翻倍，時間只增加了約一倍多一點點，並未呈現平方級數暴增。 |
| 50,000 | 0.0105 | 處理五萬筆資料依然能在極短的瞬間完成。 |
| 100,000 | 0.0221 | 即使面對十萬筆大規模資料，合併排序法依舊能保持優異的效能，完美展現了 $O(n \log n)$ 的強大優勢。

## 合併排序法
#### 1. 簡述原理

合併排序法採用了**「分而治之」 (Divide and Conquer)** 的策略。它的核心思想是將一個大問題分解成許多小問題，解決小問題後，再將結果合併起來。
演算法的運作步驟如下：
1. **分割 (Divide)：** 將未排序的數列從中間切分成兩個子數列，一直重複切分，直到每個子數列都只剩下 1 個元素為止（只有一個元素的數列視為已排序）。
2. **合併 (Merge)：** 將已排序的子數列兩兩合併。在合併的過程中，會比較兩個子數列的最前端元素，將較小的元素依序放入新的陣列中，直到所有子數列都被合併回一個完整的排序數列。

#### 2. 複雜度分析

* **時間複雜度 (Time Complexity):**
    * **最佳情況 (Best Case):** $O(n \log n)$。
    * **最壞情況 (Worst Case):** $O(n \log n)$。
    * **平均情況 (Average Case):** $O(n \log n)$。
    * *說明：無論輸入資料的初始狀態為何，合併排序法都會將數列切分 \log_2 n 次，且每次合併都需要走訪 n 個元素，因此時間複雜度始終保持在 O(n \log n)，非常穩定且高效。*
* **空間複雜度 (Space Complexity):**
    * $O(n)$。合併排序法在「合併」的步驟中，需要配置與原始數列相同大小的額外記憶體空間來暫存合併後的結果，因此**不是**原地排序。
* **穩定性 (Stability):**
    * **穩定 (Stable)**。在合併兩個子數列時，如果遇到相等的元素，通常會先將左邊（原本在前方）的元素放入陣列，因此相同大小元素的相對位置不會改變。

#### 3. 模擬實作內容與執行時間分析

**C 語言實作程式碼：**
```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

// 合併兩個已排序的子陣列
void merge(int arr[], int left, int mid, int right) {
    int i, j, k;
    int n1 = mid - left + 1;
    int n2 = right - mid;

    // 建立暫存陣列
    int *L = (int*)malloc(n1 * sizeof(int));
    int *R = (int*)malloc(n2 * sizeof(int));

    // 複製資料到暫存陣列 L[] 和 R[]
    for (i = 0; i < n1; i++) L[i] = arr[left + i];
    for (j = 0; j < n2; j++) R[j] = arr[mid + 1 + j];

    // 將暫存陣列合併回原陣列 arr[left..right]
    i = 0; j = 0; k = left;
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            arr[k] = L[i];
            i++;
        } else {
            arr[k] = R[j];
            j++;
        }
        k++;
    }

    // 將 L[] 剩餘的元素複製過去
    while (i < n1) {
        arr[k] = L[i];
        i++;
        k++;
    }

    // 將 R[] 剩餘的元素複製過去
    while (j < n2) {
        arr[k] = R[j];
        j++;
        k++;
    }
    
    free(L);
    free(R);
}

// 合併排序主函式
void mergeSort(int arr[], int left, int right) {
    if (left < right) {
        int mid = left + (right - left) / 2;

        mergeSort(arr, left, mid);      // 排序左半邊
        mergeSort(arr, mid + 1, right); // 排序右半邊
        merge(arr, left, mid, right);   // 合併兩半
    }
}

int main() {
    int n = 100000; // 測試較大的資料量
    int *arr = (int*)malloc(n * sizeof(int));
    
    // 產生隨機亂數資料
    for(int i = 0; i < n; i++) {
        arr[i] = rand() % 100000; 
    }

    // 記錄開始時間
    clock_t start_time = clock();
    
    // 執行合併排序
    mergeSort(arr, 0, n - 1);
    
    // 記錄結束時間
    clock_t end_time = clock();
    
    // 計算執行時間 (秒)
    double time_spent = (double)(end_time - start_time) / CLOCKS_PER_SEC;
    printf("資料數量: %d, 執行時間: %f 秒\n", n, time_spent);
    
    free(arr);
    return 0;
}
```
**執行時間測試結果：**

| 資料數量 ($n$) | 執行時間 (秒) | 觀察與分析 |
| :---: | :---: | :--- |
| 10,000 | 0.0018 | 相比於前幾種 $O(n^2)$ 演算法，合併排序在此資料量下的時間幾乎可以忽略不計。 |
| 20,000 | 0.0039 | 資料量翻倍，時間只增加了約一倍多一點點，並未呈現平方級數暴增。 |
| 50,000 | 0.0105 | 處理五萬筆資料依然能在極短的瞬間完成。 |
| 100,000 | 0.0221 | 即使面對十萬筆大規模資料，合併排序法依舊能保持優異的效能，完美展現了 $O(n \log n)$ 的強大優勢。 |

## 桶排序法
#### 1. 簡述原理

桶排序法的核心思想是「分組處理」。它的運作原理是將數列的值域劃分為有限數量的區間，這些區間被稱為「桶子 (Buckets)」。
演算法的運作步驟如下：
1. **設置桶子：** 根據資料的範圍與數量，建立一定數量的空桶子。
2. **分配 (Scatter)：** 走訪原始陣列，根據一定的映射函數（例如數值大小的比例），將每個元素放入對應的桶子中。
3. **桶內排序：** 對每個非空的桶子內部進行排序（通常可以使用插入排序法，或是遞迴呼叫其他排序演算法）。
4. **合併 (Gather)：** 按照桶子的順序，依序將所有桶子內的元素取出來，放回原本的陣列中，即完成排序。

#### 2. 複雜度分析

* **時間複雜度 (Time Complexity):**
    * **最佳情況 (Best Case):** $O(n + k)$（$n$ 為資料量，$k$ 為桶子數量）。當資料均勻分佈在各個桶子中，每個桶子只有極少數元素，桶內排序的時間趨近於線性。
    * **最壞情況 (Worst Case):** $O(n^2)$。當所有資料都被分配到同一個桶子裡，且桶內排序採用插入排序法時，就會退化成 $O(n^2)$ 的時間複雜度。
    * **平均情況 (Average Case):** $O(n + k)$。在資料呈現均勻分佈的前提下，平均時間複雜度為線性時間，非常高效。
* **空間複雜度 (Space Complexity):**
    * $O(n + k)$。需要額外配置 $k$ 個桶子的空間，以及儲存 $n$ 個元素的內部結構（如鏈結串列或動態陣列），因此**不是**原地排序。
* **穩定性 (Stability):**
    * **穩定 (Stable)**。只要在「桶內排序」時所使用的演算法（如插入排序）是穩定的，那麼整個桶排序法就會是穩定的。

#### 3. 模擬實作內容與執行時間分析

在 C 語言中，通常會使用「陣列搭配鏈結串列 (Linked List)」來實作桶子，以動態處理每個桶子分配到的不同資料量。

**C 語言實作程式碼：**
```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

// 定義鏈結串列節點，用於桶子內部的資料儲存
struct Node {
    int data;
    struct Node* next;
};

// 將資料插入並保持鏈結串列由小到大排序 (相當於對桶內進行插入排序)
void insertSorted(struct Node** head, int val) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    newNode->data = val;
    newNode->next = NULL;

    // 如果串列為空，或者新節點的值小於首節點，則插入在最前面
    if (*head == NULL || (*head)->data >= val) {
        newNode->next = *head;
        *head = newNode;
    } else {
        struct Node* current = *head;
        // 尋找適當的插入位置
        while (current->next != NULL && current->next->data < val) {
            current = current->next;
        }
        newNode->next = current->next;
        current->next = newNode;
    }
}

// 桶排序主函式
void bucketSort(int arr[], int n) {
    int i;
    int num_buckets = 100; // 假設設定 100 個桶子
    
    // 配置桶子陣列 (每個元素都是一個指標，指向鏈結串列的開頭)
    struct Node** buckets = (struct Node**)calloc(num_buckets, sizeof(struct Node*));

    // 找出陣列中的最大值，用於計算分配比例
    int max_val = arr[0];
    for (i = 1; i < n; i++) {
        if (arr[i] > max_val) max_val = arr[i];
    }

    // 1. 分配：將陣列元素依比例放入對應的桶子
    for (i = 0; i < n; i++) {
        // 計算該元素應該放入哪個桶子 (0 到 num_buckets-1)
        int idx = (arr[i] * num_buckets) / (max_val + 1);
        if (idx >= num_buckets) idx = num_buckets - 1; 
        
        // 放入桶子時同步進行插入排序
        insertSorted(&buckets[idx], arr[i]);
    }

    // 2. 合併：按照桶子順序，將元素依序存回原陣列
    int index = 0;
    for (i = 0; i < num_buckets; i++) {
        struct Node* current = buckets[i];
        while (current != NULL) {
            arr[index++] = current->data;
            struct Node* temp = current;
            current = current->next;
            free(temp); // 釋放記憶體避免 Memory Leak
        }
    }
    free(buckets); // 釋放桶子陣列
}

int main() {
    int n = 100000; // 測試較大的資料量
    int *arr = (int*)malloc(n * sizeof(int));
    
    // 產生隨機均勻分佈的亂數資料
    for(int i = 0; i < n; i++) {
        arr[i] = rand() % 100000; 
    }

    // 記錄開始時間
    clock_t start_time = clock();
    
    // 執行桶排序
    bucketSort(arr, n);
    
    // 記錄結束時間
    clock_t end_time = clock();
    
    // 計算執行時間 (秒)
    double time_spent = (double)(end_time - start_time) / CLOCKS_PER_SEC;
    printf("資料數量: %d, 執行時間: %f 秒\n", n, time_spent);
    
    free(arr);
    return 0;
}
```
**執行時間測試結果：**

| 資料數量 (n) | 執行時間 (秒) | 觀察與分析 |
|:---:|:---:|:---|
| 10,000 | 0.00648 | 速度極快。因為資料均勻分佈，分配到各桶子後，桶內排序的負擔極小。 |
| 20,000 | 0.01503 | 資料量翻倍，時間大約增加兩倍多，呈現線性成長。 |
| 50,000 | 0.04677 | 在五萬筆資料下，效能依舊非常優異，表現直逼 $O(n \log n)$ 的演算法。 |
| 100,000 | 0.08369 | 面對十萬筆資料，在資料「分佈均勻」的理想條件下，時間複雜度展現出接近線性 $O(n)$ 的強大優勢。但若資料極度不均勻，效能將大幅退化。 |

## 綜合比較
經過上述各種排序演算法的原理介紹與實作模擬，我們將這五種演算法的複雜度與特性整理成下表，以便進行綜合比較：

| 演算法名稱 | 最佳時間複雜度 | 最壞時間複雜度 | 平均時間複雜度 | 空間複雜度 | 穩定性 | 適用情境分析 |
| :--- | :---: | :---: | :---: | :---: | :---: | :--- |
| **氣泡排序法** (Bubble Sort) | $O(n)$ | $O(n^2)$ | $O(n^2)$ | $O(1)$ | 穩定 | 實作最簡單，適合資料量極小，或教學示範用途。 |
| **選擇排序法** (Selection Sort) | $O(n^2)$ | $O(n^2)$ | $O(n^2)$ | $O(1)$ | 不穩定 | 交換次數少於氣泡排序，但整體效能仍差，適合資料量小的場景。 |
| **插入排序法** (Insertion Sort) | $O(n)$ | $O(n^2)$ | $O(n^2)$ | $O(1)$ | 穩定 | 適合資料量小，且**「資料幾乎已經排好序」**的情況，此時效能極佳。 |
| **合併排序法** (Merge Sort) | $O(n \log n)$ | $O(n \log n)$ | $O(n \log n)$ | $O(n)$ | 穩定 | 效能非常穩定且極快，適合處理**大規模資料**，但需消耗額外的記憶體空間。 |
| **桶排序法** (Bucket Sort) | $O(n+k)$ | $O(n^2)$ | $O(n+k)$ | $O(n+k)$ | 穩定 | 當資料呈現**均勻分佈**時效能最好，逼近線性時間，但極度依賴資料的分佈型態與桶子設計。 |

#### 綜合效能觀察總結：

1. **小規模資料 ($O(n^2)$ 演算法)：** 氣泡排序、選擇排序與插入排序這三者的平均時間複雜度皆為 $O(n^2)$，在資料量上萬筆時會出現明顯的效能瓶頸。但在資料量極小或已局部排序的情況下，插入排序法通常會有不錯的表現，且它們都具備 $O(1)$ 的空間優勢（不需要額外記憶體）。
2. **大規模資料 ($O(n \log n)$ 演算法)：** 合併排序法展現了強大的穩定性與速度，面對十萬筆以上的資料依然能瞬間完成。雖然需要付出 $O(n)$ 的空間代價，但在現代電腦記憶體充足的環境下，通常是極具性價比的選擇。
3. **特定分佈資料 (線性時間演算法)：** 桶排序法突破了比較排序法 $O(n \log n)$ 的極限。在我們模擬的「均勻分佈亂數」測試中，表現甚至優於合併排序。但必須注意，如果資料集中在少數幾個區間（極度不均勻），它的效能將會退化。
 
## 學習心得
透過這次的排序演算法模擬報告，我對資料結構與演算法的效能差異有了更深刻的體會。將課堂上的理論轉化為實際的 C 語言程式碼，並親自測量巨量資料的執行時間，讓我清楚看見 $O(n^2)$ 與 $O(n \log n)$ 之間巨大的效能落差，也更明白在不同情境下選擇合適演算法的重要性。

除了演算法本身的理論知識，這次作業更是對現代軟體開發工具的一次完整實戰演練。我使用了 VSCode 作為主要的開發環境，並實際操作了如何透過內建介面使用 Git 進行版本控制，順利將本地端的專案與遠端的 GitHub 連結，並成功推送到 GitHub 數據庫上。這套完整的流程讓我對程式碼管理有了更具體的概念，也體會到版本控制在開發上的便利性。

在開發的過程中，我也遇到了一段小插曲。我原本有使用 GitHub Copilot 這類 AI 工具來輔助撰寫程式碼與加速除錯，但寫到一半時，卻突然發生 Copilot 權限被終止、無法使用的狀況。經過一番問題排查與了解，才發現是因為我的學生身分認證過期了。最終的解決方法是親自到 GitHub Education 重新提交相關證明進行申請，待審核通過後，才順利恢復了 Copilot 的使用權限。這個突發狀況雖然稍微打斷了開發節奏，但也讓我學會了如何處理開發環境與帳號授權的異常問題。

總結來說，這次的報告不僅讓我扎實地複習了五種排序演算法的實作與複雜度分析，更讓我在 VSCode 環境設定、Git 與 GitHub 的連動操作，以及臨場排除開發工具障礙等方面，都累積了相當寶貴的實務經驗，是一次非常充實的學習歷程。
