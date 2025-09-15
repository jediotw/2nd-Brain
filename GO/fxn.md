package main

  

import (

    "fmt"

)

  

func learningfxn() {

    fmt.Println("I am Learning Function")

  

    // declaring an inner function using function literals

    inner := func() string {

        return "I am Inner Function"

    }

  

    inner2 := func() string {

        return "I am Inner2 Function"

    }

  

    fmt.Println(inner())

    fmt.Println(inner2())

  

    username, age := getUserByID(1)

    fmt.Printf("name %v age %v", username, age)

  

    username1, age1 := getUserByID2(1)

    fmt.Printf("name %v age %v", username1, age1)

  

    value := add()

    fmt.Println(value)

  

    total := sum(1, 2, 3, 4, 5)

    fmt.Println("Total:", total)

  

    concateFullName := func(firstName, lastName string) string {

        return fmt.Sprintf("%s %s", firstName, lastName)

    }

    fmt.Println(concateFullName("Saurabh", "Kumar"))

}

  

// getUserByID returns a dummy username and age for demonstration

func getUserByID(id int) (string, int) {

    fmt.Println(id)

    return "SaurabhKumar", 30

}

func getUserByID2(id int) (name string, age int) {

    fmt.Println(id)

    return "SaurabhKumar", 30

}

  

func add() string {

    return "i am a add function"

}

  

// if don't know the number of inputs use ... before the datatype

func sum(numbers ...int) int {

    total := 0

    for _, number := range numbers {

        total += number

    }

    return total

}

  

//