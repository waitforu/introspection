# 选择排序
### SortInterface.php
```php

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
### SelectionSort.php
```php
namespace common\algorithms\sorts;

class SelectionSort extends SortSwap implements SortInterface{
    private $array; // 需要排序的数组
    static public $instance; //
    // TODO: Implement sort() method.
    public function sort()
    {
        $len = count($this->array);
        // echo microtime().'<br/>';
        for($i = 0; $i < $len; $i++){
            $min = $i;
            for($j = $i+1; $j < $len; $j++){
                if($this->array[$min] > $this->array[$j]){
                    $min = $j;
                }
            }
            if($min != $i){
                self::swap($this->array[$min], $this->array[$i]);
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