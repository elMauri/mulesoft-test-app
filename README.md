<p align="center">
  <img width="300" height="300" src="https://www.cloudfoundry.org/wp-content/uploads/2017/10/icon_mulesoft@2x.png">
</p>

# Mulesoft Technical Excersice

## Overview 
A simple Mule project is designed to show us that you can learn mule quickly and present your
project to the services team.

## Getting started
Create a simple REST web service that will access that database and be able to:
- Retrieve all the " filled " orders data including the net amount of each transaction (given
the quantity of shares and the price).
- Insert a new " BUY " or " SELL " order into the table with the status " Pending ".

## Built in
* [Anypoint Studio](https://www.mulesoft.com/lp/dl/studio)
* [Java](https://www.java.com/es/download/)
* [Apache Maven](https://maven.apache.org/)
* [Git](https://github.com/)
* [Spring framework](https://spring.io/)
* [MySQL](https://www.mysql.com/)

## Installing
Locate in some place on your PC and execute:

```
git clone https://github.com/elMauri/mulesoft-test-app
cd mulesoft.challenge.app
mvn clean package
```
In Windows:
```
java -jar target\mulesoft.challenge.app-1.0.0-SNAPSHOT-mule-application.jar
```
In Linux:
```
java -jar target/mulesoft.challenge.app-1.0.0-SNAPSHOT-mule-application.jar
```

## Exposing

Application has two Api's exposed:

### **1. Service:**

```
“/api/orders”
```
Retrieve all the " filled " orders data including the net amount of each transaction (given
the quantity of shares and the price).

**HTTP Method**: GET → /api/orders/  

Response e.g.:
```
[
    {
        "ORDER_DATE": "2018-02-08T18:40:50",
        "SYMBOL": "DIA",
        "QUANTITY": 505,
        "PRICE": 107.8499984741211,
        "ACTION": "BUY",
        "NET_AMOUNT": 54464.25,
        "TX_NUMBER": 82,
        "STATUS": "Filled"
    },
    {
        "ORDER_DATE": "2018-10-06T22:58:30",
        "SYMBOL": "DIA",
        "QUANTITY": 3526,
        "PRICE": 899.72998046875,
        "ACTION": "SELL",
        "NET_AMOUNT": 3172447.91,
        "TX_NUMBER": 101,
        "STATUS": "Filled"
    },
    {
        "ORDER_DATE": "2017-11-11T19:15:22",
        "SYMBOL": "DIA",
        "QUANTITY": 1581,
        "PRICE": 566.1300048828125,
        "ACTION": "SELL",
        "NET_AMOUNT": 895051.54,
        "TX_NUMBER": 113,
        "STATUS": "Filled"
    }
...
]
```


#### HTTP status code handling:

* **HTTP 200-OK** : _Retrieved all Orders_.  
* **HTTP 401-Unauthorized** : _When the username o password not exists_. 

```
{
    "message": "Invalid Credentials"
}
```

* **HTTP 401-Unauthorized** :_When the username has not right grants to execute the resource_. 
````
{
    "message": "Unauthorized user: [username]"
}
````
### **2. Service:**
```
“/api/order”
```
**HTTP Method**: POST → /api/order/  

This Api require send a JSON payload via POST verb with specific format and mandatory fields:
```
  tx_number?: number
  order_date: 
    type: datetime-only
    example: 2015-07-04T21:00:00
  quantity: number
  price: number
  symbol: string
  action: 
    description: Type of Action
    enum: [BUY,SELL]
  status?: 
    description: Type of Status
    enum: [Pending, Filled, Canceled]
```
#### HTTP status code handling:

* **HTTP 200-OK** : _When the order is correctly inserted_.
```
{
    "message": "The Order has been properly entered"
}

```
* **HTTP 400-BAD REQUEST** : _When recieve malformed or unexpected JSON payload_. 
````
{
    "message": "Bad request"
}
````
* **HTTP 409-CONFLICT** : _When the input Order already exists_. 
````
{
    "message": "Order already exists"
}
````
* **HTTP 401-Unauthorized** : _When the username o password not exists_. 

```
{
    "message": "Invalid Credentials"
}
```

* **HTTP 401-Unauthorized** :_When the username has not right grants to execute the resource_. 
````
{
    "message": "Unauthorized user: [username]"
}
```` 


## Autor
* **Mauricio Borelli** - *Intial work and documentation*