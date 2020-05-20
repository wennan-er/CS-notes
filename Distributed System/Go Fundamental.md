# Go Fundamental  

## Methods And Interfaces  

### Struct  
```go
type person struct {
    name string
    age  int
}
```
```go
func newPerson(name string) *person {
    p := person{name: name}
    p.age = 42
    return &p
}
//You can safely return a pointer to local variable as a local variable will survive the scope of the function.
```