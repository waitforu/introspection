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
```
<?php

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
```
<?php
namespace common\algorithms\sorts;

class BubbleSort extends SortSwap implements SortInterface{
    private $array; // 需要排序的数组
    static public $instance; //
    //static public $temp;
    // TODO: Implement sort() method.
    public function sort()
    {
        $len = count($this->array);
        // echo microtime().'<br/>';
        for($i = 0; $i < $len - 1; $i++){
            for($j = $len - 1; $j > $i; $j--){
                if($this->array[$j-1] > $this->array[$j]){
                    self::swap($this->array[$j-1], $this->array[$j]);
                }
            }
            // echo implode(',',$this->array).'<br/>';
        }
        // echo microtime().'<br/>';
        return $this->array;
    }

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