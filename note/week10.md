#　第十周

## 单行程系统与多工系统

![1](https://github.com/lzc2021/sp109b/blob/main/image/06.png)

## 協同式多工系統
* 看似多工系統，但實際上任何一個程式當機都會導致系統失效，非真正多工系統。
* 又稱偽多工系統。
* Ex: windows3.1

## 競爭情況 (race condition)
* 電腦中的兩個行程同時試圖修改一個共享記憶體的內容，則最後的結果是不正確的。
![race_condition](https://user-images.githubusercontent.com/62127656/120276560-6f90ec00-c2e5-11eb-8599-3c62e7e13b01.jpg)

## 死結 (deadlock)
* 兩個以上的運算單元，雙方都在等待對方停止執行，以取得系統資源，但是沒有一方提前退出時，就稱為死結。

## 作业系统行程

![1](https://github.com/lzc2021/sp109b/blob/main/image/07.jpg)

