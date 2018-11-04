# 冒泡排序
## 原理
对数组相邻两个元素进行比较，根据大小互换位置，每次冒泡让至少一个元素移动到它该处在的位置，n个数据，重复n次冒泡。
### SortInterface.php
```
<?php

namespace common\algorithms\sorts;

interface SortInterface{
    /**
     * 对传入的原始数组进行排序
     * @return array 返回排序好的数组
    */
    public function sort();
}
```
### SortSwap.php
```php
namespace common\algorithms\sorts;

class SortSwap{
    static public $temp;
    static public function swap(&$a, &$b){
        self::$temp = $a;
        $a = $b;
        $b = self::$temp;
    }
}
```
### BubbleSort.php
```php
<?php
namespace common\algorithms\sorts;

class BubbleSort extends SortSwap implements SortInterface{
    private $array; // 需要排序的数组
    static public $instance; //
    // TODO: Implement sort() method.
    /**
     * 方法一：最大值后移
     */
    public function sort()
    {
        $len = count($this->array);
        for($i = 0; $i < $len - 1; $i++){
            for($j = 0; $j < $len - 1 - $i; $j++){
                if($this->array[$j] > $this->array[$j+1]){
                    self::swap($this->array[$j+1], $this->array[$j]);
                }
            }
        }
        return $this->array;
    }
    /**
     * 方法二：最小值前移
     *
    public function sort()
    {
        $len = count($this->array);
        for($i = 0; $i < $len - 1; $i++){
            for($j = $len - 1; $j > $i; $j--){
                if($this->array[$j-1] > $this->array[$j]){
                    self::swap($this->array[$j-1], $this->array[$j]);
                }
            }
        }
        return $this->array;
    }
    */

    static public function getInstance(){
        if(!self::$instance) self::$instance = new self();
        return self::$instance;
    }

    public function getSorts($array){
        $this->array = $array;
        return $this->sort();
    }
}
```
## 优化
如果在某次冒泡没有进行交换数据，则说明数据已经是一个有序数组，不需要再进行下一次的冒泡了，这时候就可以结束冒泡操作。
### 优化代码(排序部分)
```php
    public function sort()
    {
        $len = count($this->array);
        for($i = 0; $i < $len - 1; $i++){
            $flag = false; // 默认数据没有进行交换
            for($j = 0; $j < $len - 1 - $i; $j++){
                if($this->array[$j] > $this->array[$j+1]){
                    self::swap($this->array[$j+1], $this->array[$j]);
                    $flag = true; // 如果进行交换则flag赋值为true
                }
            }
            if(!$flag) break; // 如果已经没有交换了则跳出循环
        }
        return $this->array;
    }
```