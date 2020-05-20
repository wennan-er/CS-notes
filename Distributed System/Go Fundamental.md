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
* Example  
```go
r := rect{width: 10, height: 5}  
r.area(), r.perim()
```

### Interface  

* An interface type is defined by a set of methods. A value of interface type can hold any value that implements those methods.  

```go
type geometry interface {
    area() float64
    perim() float64
}
//For our example we’ll implement this interface on rect and circle types.
type rect struct {
    width, height float64
}
type circle struct {
    radius float64
}
```
* To implement an interface in Go, we just need to implement all the methods in the interface. Here we implement geometry on rects.  

```go
func (r rect) area() float64 {
    return r.width * r.height
}
func (r rect) perim() float64 {
    return 2*r.width + 2*r.height
}

func (c circle) area() float64 {
    return math.Pi * c.radius * c.radius
}
func (c circle) perim() float64 {
    return 2 * math.Pi * c.radius
}
``` 

* If a variable has an interface type, then we can call methods that are in the named interface.  
* The circle and rect struct types both implement the geometry interface so we can use instances of these structs as arguments to measure.    
```go
func measure(g geometry) {
    fmt.Println(g)
    fmt.Println(g.area())
    fmt.Println(g.perim())
}
func main() {
    r := rect{width: 3, height: 4}
    c := circle{radius: 5}
    measure(r)
    measure(c)
}
```

## Concurrency  

### Goroutines
* A goroutine is a lightweight thread of execution.  
* To invoke this function in a goroutine, use ```go f(s)```.  

### Channels  
* Channels are the pipes that connect concurrent goroutines.  
* You can send values into channels from one goroutine and receive those values into another goroutine.  
* Send a value into a channel using the channel <- syntax.  

#### Blocking Channel  
```go
func main() {
    messages := make(chan string)
    go func() { messages <- "ping" }()
    msg := <-messages
    fmt.Println(msg)
}
```
* By default sends and receives block until both the sender and receiver are ready.  
  * Here one thread is ```go msg := <-messages ``` waiting for receiving from channel.  
  * One thread we create ```go go func() { messages <- "ping" }() ``` is sending to channel.  

#### Channel Buffering  
```go
func main() {
    messages := make(chan string, 2)

    messages <- "buffered"
    messages <- "channel"

    fmt.Println(<-messages)
    fmt.Println(<-messages)
}
```
* Because this channel is buffered by 2 values, when it is full, we can send these values into the channel without a corresponding concurrent receive.  

#### Channel Directions
```go
func ping(pings chan<- string, msg string) {
    pings <- msg
}
// The pong function accepts one channel for receives (pings) and a second for sends (pongs).
func pong(pings <-chan string, pongs chan<- string) {
    msg := <-pings
    pongs <- msg
}
func main() {
    pings := make(chan string, 1)
    pongs := make(chan string, 1)
    ping(pings, "passed message")
    pong(pings, pongs)
    fmt.Println(<-pongs)
}
```
* ```go pings <-chan string ```: channel for sending.    
* ```pongs chan<- string ```: channel for receiving.  

#### Select:wait on multiple channel operations

```go
func main() {
    c1 := make(chan string)
    c2 := make(chan string)

    go func() {
        time.Sleep(1 * time.Second)
        c1 <- "one"
    }()
    go func() {
        time.Sleep(2 * time.Second)
        c2 <- "two"
    }()

    for i := 0; i < 2; i++ {
        select {
        case msg1 := <-c1:
            fmt.Println("received", msg1)
        case msg2 := <-c2:
            fmt.Println("received", msg2)
        }
    }
}
```
#### WaitGroups
```go
func worker(id int, wg *sync.WaitGroup) {

    defer wg.Done()
    fmt.Printf("Worker %d starting\n", id)

    time.Sleep(time.Second)
    fmt.Printf("Worker %d done\n", id)
}

func main() {
    var wg sync.WaitGroup

    for i := 1; i <= 5; i++ {
        wg.Add(1)
        go worker(i, &wg)
    }
   // Block until the WaitGroup counter goes back to 0; all the workers notified they’re done.
    wg.Wait()
}
```