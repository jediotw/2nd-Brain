package main

  

import "fmt"

  

func datatype() {

    // fmt.Println("learning datatypes....")

  

    /*two types of datatype in golang

    `1. basic datatype: int ,bool ,string ,float64,float32

    2. composite datatype: array ,slice ,map ,struct

    3. reference datatype: pointer ,function ,interface ,channel

    4. user defined datatype: type ,const

    5. zero value datatype: nil

    */

    /*

        var -> whose value can be changed

        const -> whose value cannot be changed

  
  

        if any specific variable is unused then it will give an error. TO avoid that we use _ (underscore)

        if you untilize a variable then it will not give an error.

  

    */

  

    var age int = 10

    var name string = "hello"

    var isEmployee bool = true

    var Height float64 = 10.5

  

    fmt.Println(age, name, isEmployee, Height)

  

    /*

        format specifier prints with printf function

        %d -> int

        %s -> string

        %t -> bool

        %f -> float64,float32

        %v -> value

  

        \n -> new line

        \t -> tab space

        \r -> carriage return

        \" -> double quote

        \' -> single quote

        \\ -> backslash

  

    */

  

    fmt.Printf("age is : %d \n name is : %s \n isEmployee is : %t \n Height is : %f \n", age, name, isEmployee, Height)

  

    //this short hand declaration only works inside the function

    //no need to mention the datatype

    //:= is used for short hand declaration

    //cannot use := outside the function

    //cannot use var and := together

  

    //if you want to change the value of a variable then you have to use = operator

    //age:= 20 -> wrong

    //age = 20 -> correct

  

    //if you want to declare a variable without assigning a value then you have to use var keyword

    //age:= -> wrong

    //var age int -> correct

  

    //if you want to declare multiple variables then you have to use var keyword

    //a,b,c:= 1,2,3 -> wrong

    //var a,b,c int = 1,2,3 -> correct

  

    //if you want to declare a variable without specifying the datatype and assigning a value then you have to use var keyword

    //age:= -> wrong

    //var age = 10

    /*age:= 20

    name:= "world"

    isEmployee:= false

    Height:= 20.5

  

    fmt.Println(age, name, isEmployee, Height)

  

    fmt.Printf("age is : %d \n name is : %s \n isEmployee is : %t \n Height is : %f \n", age, name, isEmployee, Height)

  

    //type conversion

    var num1 int = 10

    var num2 float64 = float64(num1) //int to float64

    var num3 string = string(num1)   //int to string (ASCII value)

    var num4 int = int(num2)         //float64 to int

  

    fmt.Println(num1, num2, num3, num4)

  

    //multiple variable declaration

    var a, b, c int = 1, 2, 3

    var d, e, f string = "hello", "world", "!"

    var g, h, i bool = true, false

  

    fmt.Println(a, b, c, d, e, f, g, h, i)

  

    //multiple variable declaration without var keyword

    j, k, l := 4, 5, 6

    m, n, o := "foo", "bar", "baz"

    p, q, r := false, true

  

    fmt.Println(j, k, l, m, n, o, p, q, r)

  

    //constant declaration

    const pi float64 = 3.14

    const e string = "Euler's number"

    const isGoFun bool = true

  

    fmt.Println(pi, e, isGoFun)

  

    //iota -> it is used to create enumerated constants

    const (

        Monday    = iota //0

        Tuesday          //1

        Wednesday        //2

        Thursday         //3

        Friday           //4

        Saturday         //5

        Sunday           //6

    )

  

    fmt.Println(Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday)

  

    //zero value

    var age1 int

    var name1 string

    var isEmployee1 bool

    var Height1 float64

  

    fmt.Println(age1, name1, isEmployee1, Height1) //0 "" false 0

  

    //pointer -> it is used to store the address of a variable

    var num int = 10

    var ptr *int = &num //& -> address of operator

  

    fmt.Println(num, ptr)  //10 0xc0000140b0

    fmt.Println(num, *ptr) //10 10 -> * -> dereference operator

  

    //function as a datatype

    //function can be assigned to a variable

    //function can be passed as an argument to another function

    //function can be returned from another function

  

    add := func(a int, b int) int {

        return a + b

    }

  

    fmt.Println(add(10, 20)) //30

  

    //array -> it is used to store multiple values of the same datatype

    var arr [5]int = [5]int{1, 2, 3, 4, 5}

    var arr1 = [5]string{"hello", "world", "foo", "bar", "baz"}

    arr2 := [5]bool{true, false, true, false, true}

  

    fmt.Println(arr, arr1, arr2)

    fmt.Println(arr[0], arr1[1], arr2[2]) //1 world true

  

    //slice -> it is a dynamic array

    var slice []int = []int{1, 2, 3, 4, 5}

    slice1 := []string{"hello", "world", "foo", "bar", "baz"}

    var slice2 = []bool{true, false, true, false, true}

  

    fmt.Println(slice, slice1, slice2)

    fmt.Println(slice[0], slice1[1], slice2[2]) //1 world true

  

    //map -> it is used to store key-value pairs

    var map1 map[string]int = map[string]int{"one": 1, "two": 2, "three": 3}

    map2 := map[string]string{"name": "hello", "greet": "world"}

    var map3 = map[string]bool{"isGoFun": true, "isJavaFun": false}

  

    fmt.Println(map1, map2, map3)

    fmt.Println(map1["one"], map2["name"], map3["isGoFun"]) //1 hello true

  

    //struct -> it is used to store multiple values of different datatypes

    type Person struct {

        name   string

        age    int

        isEmployed bool

        height float64

    }

    p1 := Person{name: "hello", age: 10, isEmployed: true, height: 5.5}

    var p2 Person = Person{name: "world", age: 20, isEmployed: false, height: 6.0}

    var p3 = Person{name: "foo", age: 30, isEmployed: true, height: 5.8}

  

    fmt.Println(p1, p2, p3)

    fmt.Println(p1.name, p2.age, p3.isEmployed) //hello 20 true

  

    //interface -> it is used to store multiple values of different datatypes

    var i1 interface{} = "hello"

    var i2 interface{} = 10

    var i3 interface{} = true

  

    fmt.Println(i1, i2, i3) //hello 10 true

  

    //type assertion -> it is used to convert interface to a specific datatype

    var str string = i1.(string)

    var num4 int = i2.(int)

    var bool1 bool = i3.(bool)

  

    fmt.Println(str, num4, bool1) //hello 10 true

  

    //channel -> it is used to communicate between goroutines

    //make -> it is used to create a channel

    ch := make(chan int)

  

    //send value to channel

    go func() {

        ch <- 10

    }()

  

    //receive value from channel

    num5 := <-ch

    fmt.Println(num5) //10

  

    //pointer, function, interface, channel are reference datatypes because they store the address of the value not the value itself

  

    //user defined datatype -> it is used to create a new datatype

    type myInt int

    var num6 myInt = 10

    fmt.Println(num6) //10

  

    //const -> it is used to create a constant value

    const pi1 float64 = 3.14

    fmt.Println(pi1) //3.14

  

    //iota -> it is used to create enumerated constants

    const (

        Red = iota //0

        Green               //1

        Blue                //2

    )

  

    fmt.Println(Red, Green, Blue) //0 1 2

  

    */

  

    /*array and slice*/

    // var arr [5]int

    // arr[0] = 1

    // arr[1] = 2

    // arr[2] = 3

    // arr[3] = 4

    // arr[4] = 5

    arr := [5]int{1, 2, 3, 4, 5}

    // arr := [...]int{1, 2, 3, 4, 5} //compiler will count the length of the array

    // arr := [5]int{1, 2}           //if you don't assign value to all the elements then the remaining elements will be assigned to zero value

    // arr := [5]int{}                //all elements will be assigned to zero value

    // arr := [5]int{0: 1, 4: 5}     //you can assign value to specific index

    arr[0] = 10 //you can change the value of an element

  

    fmt.Println("array:", arr)

    fmt.Println("array length:", len(arr))

  

    //slice: size is dynamic

    // var slice []int

    // slice = append(slice, 1)

    // slice = append(slice, 2)

    // slice = append(slice, 3)

    slice := []int{1, 2, 3, 4, 5}

    slice = append(slice, 6) //you can add value to the slice using the append function

    slice[0] = 10            //you can change the value of an element

  

    fmt.Println("slice:", slice)

    fmt.Println("slice length:", len(slice))

  

    //difference between array and slice

    //1. array has a fixed size but slice has a dynamic size

    //2. array is a value type but slice is a reference type

    //3. array is stored in stack memory but slice is stored in heap memory

    //4. array can be compared but slice cannot be compared

  

    //multidimensional array

    var multiArr [2][3]int = [2][3]int{{1, 2, 3}, {4, 5, 6}}

    fmt.Println("multidimensional array:", multiArr)

  

    //multidimensional slice

    var multiSlice [][]int = [][]int{{1, 2, 3}, {4, 5, 6}}

    multiSlice = append(multiSlice, []int{7, 8, 9})

    fmt.Println("multidimensional slice:", multiSlice)

  

    mycourse := [3][2]string{

        {"go", "nodejs"},

        {"AWS", "typescript"},

        {"Kafka", "GCP"},

    }

    fmt.Printf("Available courses are %v\n", mycourse)

  

    myslicecourse := [][]string{

        {"go", "nodejs"},

        {"AWS", "typescript"},

        {"Kafka", "GCP"},

    }

    newCourse := []string{"docker", "kubernetes"}

    myslicecourse = append(myslicecourse, newCourse)

    myslicecourse = append(myslicecourse, []string{"Cloud", "IAC"})

    fmt.Printf("Available slicecourses are %v\n", myslicecourse)

  

    //helper function to craete slices

    s := make([]string, 3) //create a slice of string with length 3

    s[0] = "hello"

    s[1] = "world"

    s[2] = "!"

    fmt.Println("slice using make:", s)

  

    s1 := make([]int, 3, 5) //create a slice of int with length 3 and capacity 5

    s1[0] = 1

    s1[1] = 2

    s1[2] = 3

    fmt.Println("slice using make with capacity:", s1)

    fmt.Println("slice length:", len(s1))

    fmt.Println("slice capacity:", cap(s1)) //capacity is the total number of elements that can be stored in the slice

  

    //conditional statements

    if age > 18 {

        fmt.Println("You are an adult")

    } else {

        fmt.Println("You are a minor")

    }

  

    //switch case

    switch age {

    case 18:

        fmt.Println("You are 18 years old")

    case 20:

        fmt.Println("You are 20 years old")

    default:

        fmt.Println("You are neither 18 nor 20 years old")

    }

  

    //for loop

    for i := 0; i < 5; i++ {

        fmt.Println(i)

    }

  

    //for range loop

    for index, value := range arr {

        fmt.Printf("index: %d, value: %d\n", index, value)

    }

  

    //break and continue

    for i := 0; i < 10; i++ {

        if i == 5 {

            break //exit the loop

        }

        if i%2 == 0 {

            continue //skip the even numbers

        }

        fmt.Println(i)

    }

  

    //goto statement

    //goto can be used to jump to a specific label

    //it is not recommended to use goto statement

    //it can make the code hard to read and understand

    //it can create infinite loops

    var j int = 0

Here:

    if j < 5 {

        fmt.Println(j)

        j++

        goto Here

    }

    //end of goto statement

    //example

    age2 := 20

    if age2 < 18 {

        fmt.Println("You are a minor")

    } else if age2 >= 18 && age2 < 60 {

        fmt.Println("You are an adult")

    } else {

        fmt.Println("You are a senior citizen")

  

    }

  

    //switch case with string

    seatclass := "First"

    switch seatclass {

    case "First":

        fmt.Println("You are in First class")

    case "Business":

        fmt.Println("You are in Business class")

    case "Economy":

        fmt.Println("You are in Economy class")

    default:

        fmt.Println("Invalid seat class")

    }

    //select statement

    //it is used to select one of the multiple channel operations

    //it is similar to switch case but it is used for channels

    ch1 := make(chan string)

    ch2 := make(chan string)

  

    go func() {

        ch1 <- "Hello from ch1"

    }()

  

    go func() {

        ch2 <- "Hello from ch2"

    }()

  

    select {

    case msg1 := <-ch1:

        fmt.Println(msg1)

    case msg2 := <-ch2:

        fmt.Println(msg2)

    default:

        fmt.Println("No message received")

    }

  

    //defer statement

    //it is used to delay the execution of a function until the surrounding function returns

    //it is used to release resources like file, network connection, database connection etc.

    //it is executed in LIFO (Last In First Out) order

    defer fmt.Println("This is the first defer statement")

    defer fmt.Println("This is the second defer statement")

    defer fmt.Println("This is the third defer statement")

    fmt.Println("This is the main function")

  

    //panic and recover

    //panic is used to raise an error

    //recover is used to recover from a panic

    //it is used to handle errors gracefully

    //it is similar to try-catch block in other programming languages

  

    // defer func() {

    //  if r := recover(); r != nil {

    //      fmt.Println("Recovered from panic:", r)

    //  }

    // }()

    // panic("This is a panic message")

    // fmt.Println("This line will not be executed")

  

    //loops

  

    var myfrnds []string

  

    for i := 0; i < 10; i++ {

        myNewFrnd := fmt.Sprintf("frnd%d", i)

        myfrnds = append(myfrnds, myNewFrnd)

    }

    fmt.Println("my friends are:", myfrnds)

  

    for index, value := range myfrnds {

        fmt.Printf("index: %d, value: %s\n", index, value)

    }

  

    //do while but in for loop coz there is no do while in golang

    count := 0

    for {

        fmt.Println("count:", count)

        count++

        if count >= 5 {

            break

        }

    }

  

    //infinite loop in case of server/socket programming

    cnt := 0

    for {

        fmt.Println("I am listening to the port 9000")

        cnt++

        if cnt == 50 {

            break

        }

  

    }

  

    //pointer:it's a variable that stores the memory address of another variable mean if you have already have created a variable why again create a same thing variable . using pointer you can just point to that varibale in this way we can efficienlty manage the memory

    saurabh := "Course Purchased"

  

    var guest *string

    guest = &saurabh

  

    fmt.Println("saurabh:", saurabh)

    fmt.Println("saurabh address:", &saurabh)           //address

    fmt.Println("value at saurabh address:", *&saurabh) //dereferencing

    fmt.Println("guest:", guest)                        //address

    fmt.Println("guest:", *guest)                       //dereferencing

  

}