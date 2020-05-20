# Go Fundamental  

## Methods And Interfaces  

### Struct  
```go
type person struct {
    name string
    age  int
}
```
* Create a person struct: ```go person{name: "Alice", age: 30} ```.  
* Using a function to create a person struct: ```go newPerson("Jon") ```.  

```go
func newPerson(name string) *person {
    p := person{name: name}
    p.age = 42
    return &p
}
//You can safely return a pointer to local variable as a local variable will survive the scope of the function.
```
### Methods
* Methods defined on struct types.  
```go
type rect struct {
    width, height int
}
```  
* Methods can be defined for either pointer or value receiver types.  
  * Everytime call area(), only poniter is copied, otherwise r struct is copied, will be expansive.  
  * Method can modify the value that its receiver points to.  

```go
func (r *rect) area() int {
    return r.width * r.height
}

func (r rect) perim() int {
    return 2*r.width + 2*r.height
}
```

```go
r := rect{width: 10, height: 5}  
r.area(), r.perim()
```