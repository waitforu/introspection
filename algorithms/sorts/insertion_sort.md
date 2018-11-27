# 插入排序
## 思想
将元素分成2个区块分别为：已排区，未排区；将未排区块中的值一个个的在已排区块中比较插入在合适的位置，直到未排区块中没有元素为止。这样形成的有序数组的排序算法就是插入排序算法。
## 复杂度
1. 空间复杂度:并未需要额外的存储空间，所以空间复杂度为O(1);
2. 时间复杂度
- 最好时间复杂度: 已经排好序的数组，时间复杂度为O(1);
- 最坏时间复杂度: 数组为一个倒序数组，则相当于每次插入都要插入到第一个位置，所以对于第n个数据元素要n次比较，所以时间复杂度为O(n^2)；
- 平均时间复杂度: O(n^2)

## 代码
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
### InsertionSort.php
```php
namespace common\algorithms\sorts;

class InsertionSort implements SortInterface{
    private $array;
    static public $instance; //
    public function sort() : array
    {
        // TODO: Implement sort() method.
        $len = count($this->array);
        for ($i = 1;$i < $len; $i++){
            $current = $this->array[$i];
            for ($j = $i-1; $j >= 0 && $this->array[$j] > $current;$j--){
                $this->array[$j+1] = $this->array[$j];
            }
            $this->array[$j+1] = $current;
        }
        return $this->array;
    }

    static public function getInstance(){
        if(!self::$instance) self::$instance = new self();
        return self::$instance;
    }

    /**
     * @param $array array
     * @return array
     */
    public function getSorts($array) : array
    {
        $this->array = $array;
        return $this->sort();
    }
}
```
