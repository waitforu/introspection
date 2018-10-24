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
### QSort.php
```
<?php
namespace common\algorithms\sorts;

class QSort implements SortInterface{
    private $array;
    static public $instance;

    // TODO: Implement sort() method.
    public function sort($left = 0, $right = null)
    {
        if($left < $right){
            $base = $this->division($left, $right);
            // echo implode(',',$this->array).'<br/>';
            $this->sort($left, $base - 1);
            $this->sort($base + 1, $right);
        }
    }

    protected function division($left, $right){
        $base = $this->array[$left];
        while ($left < $right){
            while ($left < $right && $this->array[$right] >= $base)
                $right--;
            $this->array[$left] = $this->array[$right];
            while ($left < $right && $this->array[$left] <= $base)
                $left++;
            $this->array[$right] = $this->array[$left];
        }
        $this->array[$left] = $base;
        return $left;
    }

    static public function getInstance(){
        if(!self::$instance) self::$instance = new self();
        return self::$instance;
    }

    public function getSorts($array){
        $this->array = $array;
        $len = count($array);
        $this->sort(0, $len - 1);
        return $this->array;
    }
}
```