package main

  

import (

    "encoding/json"

    "fmt"

)

  

func learningmap() {

    // fmt.Println("learning map....")

  

    //map is a collection of key value pair

    //map is unordered

    //map is mutable

    //map is reference datatype

    //map is used to store data in key value pair

    //map is used to store data in no specific order

    //map is used to store data in dynamic size

  

    //syntax to declare a map

    //var mapname map[keydatatype]valuedatatype

  

    /*

        var employee map[string]int //declaration of map

  

        employee = make(map[string]int) //initialization of map

  

        //insertion of data in map

        employee["emp1"] = 1001

        employee["emp2"] = 1002

        employee["emp3"] = 1003

  

        fmt.Println(employee)

  

        //accessing the value from map

        fmt.Println("emp1 id is :", employee["emp1"])

  

        //updating the value in map

        employee["emp1"] = 1010

        fmt.Println("emp1 id is :", employee["emp1"])

  

        //deleting the value from map

        delete(employee, "emp2")

        fmt.Println(employee)

  

        //length of map

        fmt.Println("length of map is :", len(employee))

  

        //map with different datatype

        var student map[int]string

        student = make(map[int]string)

  

        student[1] = "John"

        student[2] = "Doe"

        student[3] = "Smith"

  

        fmt.Println(student)

  

        //check if key is present in map or not

        value, ok := student[2]

        if ok {

            fmt.Println("value is :", value)

        } else {

            fmt.Println("key is not present")

        }

  

        //iterate over map

        for key, value := range employee {

            fmt.Println("key is :", key, "value is :", value)

        }

  

        //clear the map

        employee = make(map[string]int)

        fmt.Println("map after clearing :", employee)

  

    */

  

    /*struct: it is used to create a user defined datatype

  

     */myWishList := make(map[string][]string)

    myWishList["first"] = []string{"Bike", "Gwagon"}

    myWishList["second"] = []string{"Mac Pro", "Iphone"}

    myWishList["third"] = []string{"900 million dollar", "Leadership position in MNC"}

    fmt.Println("My wishlist are:", myWishList)

    delete(myWishList, "second")

    fmt.Println("My wishlist after deleting second key:", myWishList)

    firstWish := myWishList["first"]

    fmt.Println("My first wishlist items are:", firstWish)

  

    //struct: it is used to create a user defined datatype

    //class vs struct

    //class -> it is used to create a user defined datatype in OOP

    //struct -> it is used to create a user defined datatype in Go

    //class -> it can have methods and properties

    //struct -> it can have only properties

    //class -> it supports inheritance

    //struct -> it does not support inheritance

    //class -> it is used to create objects

    //struct -> it is used to create instances

  

    type product struct {

        name  string

        price float64

        stock int

    }

    var p1 product = product{name: "Laptop", price: 1000.00, stock: 10}

    p2 := product{name: "Mobile", price: 500.00, stock: 20}

    p3 := product{name: "Tablet", price: 300.00, stock: 30}

  

    fmt.Println(p1, p2, p3)

    fmt.Println("Product 1 name is:", p1.name)

    fmt.Println("Product 2 price is:", p2.price)

    fmt.Println("Product 3 stock is:", p3.stock)

  

    //anonymous struct

    var p4 = struct {

        name  string

        price float64

        stock int

    }{name: "Monitor", price: 200.00, stock: 15}

  

    fmt.Println(p4)

    fmt.Println("Product 4 name is:", p4.name)

  

    //nested struct

    type address struct {

        city    string

        state   string

        country string

    }

    type customer struct {

        name    string

        age     int

        address address

    }

    c1 := customer{name: "John", age: 30, address: address{city: "New York", state: "NY", country: "USA"}}

    fmt.Println(c1)

    fmt.Println("Customer name is:", c1.name)

    fmt.Println("Customer city is:", c1.address.city)

  

    //pointer to struct

    var p5 *product = &p1

    fmt.Println(p5)

    fmt.Println("Product 5 name is:", p5.name)

  

    //modifying struct using pointer

    p5.price = 1200.00

    fmt.Println("Product 1 price after modification is:", p1.price)

  

    //struct with slice

    type order struct {

        id       int

        products []product

    }

    o1 := order{id: 1, products: []product{p1, p2}}

    fmt.Println(o1)

    fmt.Println("Order id is:", o1.id)

    fmt.Println("Order products are:", o1.products)

  

    //struct with map

    type inventory struct {

        products map[string]product

    }

    inv := inventory{products: make(map[string]product)}

    inv.products[p1.name] = p1

    inv.products[p2.name] = p2

    fmt.Println(inv)

    fmt.Println("Inventory products are:", inv.products)

  

    //struct with interface

    type item struct {

        name  string

        price interface{}

    }

    it1 := item{name: "Gadget", price: 99.99}

    it2 := item{name: "Widget", price: "29.99"}

    fmt.Println(it1, it2)

    fmt.Println("Item 1 price is:", it1.price)

    fmt.Println("Item 2 price is:", it2.price)

  

    //struct with function

    type calculator struct {

        add func(int, int) int

        sub func(int, int) int

    }

    calc := calculator{

        add: func(a int, b int) int {

            return a + b

        },

        sub: func(a int, b int) int {

            return a - b

        },

    }

    fmt.Println("Addition of 10 and 5 is:", calc.add(10, 5))

    fmt.Println("Subtraction of 10 and 5 is:", calc.sub(10, 5))

  

    //struct with embedded struct

    type employee struct {

        name   string

        age    int

        salary float64

    }

    type manager struct {

        employee

        department string

    }

    m1 := manager{employee: employee{name: "Alice", age: 35, salary: 75000.00}, department: "Sales"}

    fmt.Println(m1)

    fmt.Println("Manager name is:", m1.name)

    fmt.Println("Manager department is:", m1.department)

    fmt.Println("Manager salary is:", m1.salary)

  

    //struct with tags

    type user struct {

        name  string `json:"name"`

        email string `json:"email"`

        age   int    `json:"age"`

    }

    u1 := user{name: "Bob", email: "bob@example.com", age: 30}

    fmt.Println(u1)

    fmt.Println("User name is:", u1.name)

    fmt.Println("User email is:", u1.email)

    fmt.Println("User age is:", u1.age)

  

    // //struct with methods

    // type book struct {

    //  title  string

    //  author string

    //  price  float64

    // }

    // func (b book) display() {

    //  fmt.Println("Book title is:", b.title)

    //  fmt.Println("Book author is:", b.author)

    //  fmt.Println("Book price is:", b.price)

    // }

    // b1 := book{title: "Go Programming", author: "John Doe", price: 39.99}

    // b1.display()

  

    // //struct with constructor

    // func newProduct(name string, price float64, stock int) product {

    //  return product{name: name, price: price, stock: stock}

    // }

    // p6 := newProduct("Headphones", 150.00, 25)

    // fmt.Println(p6)

    // fmt.Println("Product 6 name is:", p6.name)

    // fmt.Println("Product 6 price is:", p6.price)

    // fmt.Println("Product 6 stock is:", p6.stock)

  

    // //struct with embedding and methods

    // type circle struct {

    //  radius float64

    // }

    // func (c circle) area() float64 {

    //  return 3.14 * c.radius * c.radius

    // }

    // type cylinder struct {

    //  circle

    //  height float64

    // }

    // func (cy cylinder) volume() float64 {

    //  return cy.circle.area() * cy.height

    // cy1 := cylinder{circle: circle{radius: 7.0}, height: 10.0}

    // fmt.Println("Cylinder volume is:", cy1.volume())

    // }

  

    //struct with JSON marshalling and unmarshalling

    // type productJSON struct {

    //  Name  string  `json:"name"`

    //  Price float64 `json:"price"`

    //  Stock int     `json:"stock"`

    // }

    // pJSON := productJSON{Name: "Camera", Price: 800.00, Stock: 5}

    // jsonData, err := json.Marshal(pJSON)

    // if err != nil {

    //  fmt.Println(err)

    // }

    // fmt.Println(string(jsonData))

    // var pUnmarshal productJSON

    // err = json.Unmarshal(jsonData, &pUnmarshal)

    // if err != nil {

    //  fmt.Println(err)

    // }

    // fmt.Println(pUnmarshal)

    // fmt.Println("Unmarshalled product name is:", pUnmarshal.Name)

    // fmt.Println("Unmarshalled product price is:", pUnmarshal.Price)

    // fmt.Println("Unmarshalled product stock is:", pUnmarshal.Stock)

  

    //struct with concurrency

    // type safeCounter struct {

    //  mu    sync.Mutex

    //  count int

    // }

    // func (sc *safeCounter) increment() {

    //  sc.mu.Lock()

    //  sc.count++

    //  sc.mu.Unlock()

    // }

    // func (sc *safeCounter) value() int {

    //  sc.mu.Lock()

    //  defer sc.mu.Unlock()

    //  return sc.count

    // }

    // sc := safeCounter{}

    // var wg sync.WaitGroup

    // for i := 0; i < 1000; i++ {

    //  wg.Add(1)

    //  go func() {

    //      defer wg.Done()

    //      sc.increment()

    //  }()

    // }

    // wg.Wait()

    // fmt.Println("Final count is:", sc.value())

  

    //struct with embedding and method overriding

    // type animal struct {

    //  name string

    // }

    // func (a animal) speak() {

    //  fmt.Println(a.name, "makes a sound")

    // }

    // type dog struct {

    //  animal

    // }

    // func (d dog) speak() {

    //  fmt.Println(d.name, "barks")

    // }

    // a1 := animal{name: "Generic Animal"}

    // a1.speak()

    // d1 := dog{animal: animal{name: "Buddy"}}

    // d1.speak()

  

    // Struct definitions

    type Details struct {

        Description  string

        Manufacturer string

        Images       string

    }

  

    type Item struct {

        Name    string

        Price   float64

        Details Details

    }

  

    type Details2 struct {

        Description  string `json:"description"`

        Manufacturer string `json:"manufacturer"`

        Images       string `json:"images"`

    }

  

    type Item2 struct {

        Name    string   `json:"name"`

        Price   float64  `json:"price"`

        Details Details2 `json:"details"`

    }

  

    // Function to create and display items

    item1 := Item{

        Name:  "Smartphone",

        Price: 699.99,

        Details: Details{

            Description:  "A high-end smartphone with a sleek design.",

            Manufacturer: "TechCorp",

            Images:       "https://example.com/smartphone.jpg",

        },

    }

    fmt.Println("Item Name:", item1.Name)

    fmt.Println("Item Price:", item1.Price)

    fmt.Println("Item Description:", item1.Details.Description)

    fmt.Println("Item Manufacturer:", item1.Details.Manufacturer)

    fmt.Println("Item Images:", item1.Details.Images)

  

    item2 := Item2{

        Name:  "Smartphone",

        Price: 699.99,

        Details: Details2{

            Description:  "A high-end smartphone with a sleek design.",

            Manufacturer: "TechCorp",

            Images:       "https://example.com/smartphone.jpg",

        },

    }

    fmt.Println("\nItem2 Name:", item2.Name)

    fmt.Println("Item2 Price:", item2.Price)

    fmt.Println("Item2 Description:", item2.Details.Description)

    fmt.Println("Item2 Manufacturer:", item2.Details.Manufacturer)

    fmt.Println("Item2 Images:", item2.Details.Images)

  

    jsonData, _ := json.MarshalIndent(item2, "", "  ")

    fmt.Println("\nItem2 JSON:\n", string(jsonData))

  

}