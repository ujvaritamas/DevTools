mkdir hello
go mod init example/hello   enable dependency tracking

go run .

import <package>
go mod tidy   ->add external module to the mod file


https://go.dev/doc/tutorial/create-module

go code gruped into packages, packages grouped into modules

In Go, a function whose name starts with a capital letter can be called by a function not in the same package. This is known in Go as an exported name.

go mod edit -replace example.com/greetings=../greetings     (local file system)
go mod tidyffranNname

_test.go

go test


https://go.dev/tour/list

https://go.dev/doc/effective_go

go return value can be named
func split(sum int) (x, y int) {
	x = sum * 4 / 9
	y = sum - x
	return
}

var can be package level or function level


A defer statement defers the execution of a function until the surrounding function returns.

panic defer recover

y :=32

x := &y

var x *int

type Vertex struct {
	X int
	Y int
}

Vertex{1, 2}
v := Vertex{1, 2}

slice (length + capacity)

len(s) - slice length
cap(s)  - size of underlying array

a := []int{1,2,3}
fmt.Println(a[:2])

create a slice with make
a := make([]int, 5)  // len(a)=5
b := make([]int, 0, 5) // len(b)=0, cap(b)=5

appending to a slice
func append(s []T, vs ...T) []T

s = append(s, 1,7)

func copy(dst, src []T) int

range -> iterate through slice or map (index, copy of the element) (key value)

for _, value := range pow {
		fmt.Printf("%d\n", value)
	}

var m map[string]Vertex

m = make(map[string]Vertex)
m[key] = elem
delete(m, key)

elem, ok = m[key]		//If key is in m, ok is true. If not, ok is false.

func compute(fn func(float64, float64) float64) float64 {
	return fn(3, 4)
}

func main() {
	hypot := func(x, y float64) float64 {
		return math.Sqrt(x*x + y*y)
	}
	fmt.Println(hypot(5, 12))

	fmt.Println(compute(hypot))
	fmt.Println(compute(math.Pow))
}


can't define class

but can define types and methods on types

type T struct {
	x int
	y string
}
// Remember: a method is just a function with a receiver argument.
func (t T) methodName() int {			//t is copy if a  (better to use pointer receiver)

}

a := T {3, "ll"}
a.methodName()
method can be daclared on non-struct type  (you can only declare a method with a receiver whose type is defined in the same package as the method. You cannot declare a method with a receiver whose type is defined in another package (which includes the built-in types such as int).)

func (t *T) methodName() int {			//if modify t the original varaiable also modified

}


Interfaces
	An interface type is defined as a set of method signatures.

type Abser interface {
	Abs() float64
}

https://go.dev/tour/methods/9

Interfaces are implemented implicitly
A type implements an interface by implementing its methods. There is no explicit declaration of intent, no "implements" keyword.

Implicit interfaces decouple the definition of an interface from its implementation, which could then appear in any package without prearrangement.