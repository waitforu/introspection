# 计数排序
计数排序是一种非比较排序，适用于有确定值域的范围的排序。由于下标为值进行排序，但当全值域并不与下标重合时，会造成资源浪费或者不够用，这时候就可以进行最小值与0的偏移量和最小最大值的差值进行确定数组大小。（下述代码为数字排序，当然如果对某些特殊字符或者字符串进行排序的）
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
### CountingSort.php
```php
namespace common\algorithms\sorts;

class CountingSort implements SortInterface{
    private $array; // 需要排序的数组
    private $min; // 数组最小值
    private $max; // 数组最大值
    private $len; // 最大最小值差值，即计数数组长度
    static public $instance; //
    public function sort() : array
    {
        // TODO: Implement sort() method.
        // 初始化计数数组
        for ($i = 0; $i <= $this->len; $i++){
            $sort[$i] = 0;
        }
        $length = count($this->array); // 获取原数组长度
        // 根据数组偏移量对计数数组进行设置
        for ($j = 0; $j < $length; $j++){
            $sort[$this->array[$j] - $this->min]++;
        }
        echo $sort[$i-1];
        $result = [];
        $j = 0;
        for ($i = 0; $i <= $this->len; $i++){
            while ($sort[$i] > 0){
                $result[$j] = $i + $this->min;
                $j++;
                $sort[$i]--;
            }
        }
        return $result;
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
        $length = count($array);
        $this->array = $array;
        $this->min = $this->max = $array[0];
        for ($i = 1; $i < $length; $i++){
            if($array[$i] > $this->max) {
                $this->max = $array[$i];
                continue;
            }
            if($array[$i] < $this->min)
                $this->min = $array[$i];
        }
        $this->len = $this->max - $this->min;
        return $this->sort();
    }
}
```
