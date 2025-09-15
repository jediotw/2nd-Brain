package main

  

import (

    "fmt"

)

  

type Product struct {

    Name  string

    Price float64

    Stock int

}

  

// main fxn for this file

func learningReceiverfxn() {

    p := Product{

        Name:  "Laptop",

        Price: 999.99,

        Stock: 10,

    }

    fmt.Printf("total Amount %f", p.calculate(2))

    p.updateStock(20)

    fmt.Println("After updating stock")

    p.reduceStock(5)

    fmt.Println("After reducing stock")

    fmt.Printf("Final Stock: %d\n", p.Stock)

}

  

// fxn

func (p Product) calculate(quantity int) float64 {

    fmt.Printf("Product Name: %s\nPrice: %.2f\nStock: %d\n", p.Name, p.Price, p.Stock)

    return p.Price * float64(quantity)

}

func (p *Product) updateStock(newStock int) {

    p.Stock = newStock

}

func (p *Product) reduceStock(reduceBy int) {

    if reduceBy > p.Stock {

        fmt.Println("Insufficient stock to reduce")

        return

    }

    p.Stock -= reduceBy

}