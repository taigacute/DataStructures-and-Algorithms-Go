## 外壳排序

外壳排序算法对集合中不按顺序排列的一对元素进行排序。 要比较的元素之间的距离依次减小。 与快速排序算法

相比，该算法执行的操作更多，并且具有更高的高速缓存未命中率。在下面的代码中，我们可以看到外壳排序算法

的实现。 ShellSorter函数将整数数组作为参数并对其进行排序：

```go
//main package has examples shown
// in Go Data Structures and algorithms book
package main

// importing fmt and bytes package
import (
	"fmt"
)

// shell sorter method
func ShellSorter(elements []int) {
	var (
		n         = len(elements)
		intervals = []int{1}
		k         = 1
	)
	for {
		var interval int
		interval = power(2, k) + 1
		if interval > n-1 {
			break
		}
		intervals = append([]int{interval}, intervals...)
		k++
	}
	var interval int
	for _, interval = range intervals {
		var i int
		for i = interval; i < n; i += interval {
			var j int
			j = i
			for j > 0 {
				if elements[j-interval] > elements[j] {
					elements[j-interval], elements[j] = elements[j], elements[j-interval]
				}
				j = j - interval
			}
		}
	}
}
```

POWER方法以指数和指数为参数，将指数的幂返回给指数，如下所示：

```go
//power function
func power(exponent int, index int) int {
	var power int
	power = 1
	for index > 0 {
		if index&1 != 0 {
			power *= exponent
		}
		index >>= 1
		exponent *= exponent
	}
	return power
}
```

Main函数

```go
// main method
func main() {
	var elements []int
	elements = []int{34, 202, 13, 19, 6, 5, 1, 43, 506, 12, 20, 28, 17, 100, 25, 4, 5, 97, 1000, 27}
	ShellSorter(elements)
	fmt.Println(elements)
}
```

`go run sorting_shell.go` 输出:

```
[1 4 5 5 6 12 13 17 19 20 25 27 28 34 43 97 100 202 506 1000]
```