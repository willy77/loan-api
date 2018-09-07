
# loan-application API

Loan application is a simple API allowing consumers to subscribe a loan.

![alt text](https://github.com/willy77/loan-api/blob/master/model.jpg?raw=true)

 - All amounts are in cts.
 - All rates are multiplied by 10000

Each request allows you to add the following headers:
- The `X-transactionId` header allows you to send your transaction id, in order to help us when debuging.


## Loan request [/loan_requests/{request_id}]

### Retrieve the loan object [GET]

Retreive a loan request


+ Parameters
    + request_id (string, required) - ID of the loan request
+ Response 200 (application/json)
   When  found
    + Headers
    
            X-transactionId: 123456789
            X-test-mode: true
        
    + Attributes (LoanRequest)

+ Response 404 (application/json)
    Not  found
    + Headers
    
            X-transactionId: 123456789
            X-test-mode: true

## Loan requests Collection [/loan_requests]

### create a new loan request [POST]

Creates a loan request

- The `X-test-mode` header allow us to run the loan application in test mode, and the resulting proposal will not be taken in account.

+ Request
    + Headers
    
            X-transactionId: 123456789
            X-test-mode: true
            
    + Attributes (LoanRequest)
    
+ Response 201 (application/json)
    + Headers

            X-transactionId: 123456789
            X-test-mode: true
            Location: loan_requests/{request_id}

## Loan request Simulation Collection [/loan_requests/{request_id}/simulations]

### create a new loan request simulations [POST]

Creates a loan request simulation

+ Parameters
    + request_id (string, required) - ID of the loan request

+ Request
    + Headers
    
            X-transactionId: 123456789

    + Attributes (CustomisationContext)
    
+ Response 201 (application/json)
    + Headers

            X-transactionId: 123456789
            X-test-mode: true
            Location: loan_requests/{request_id}/simulations

### Retreive simulations result [GET]

+ Parameters
    + request_id (string, required) - ID of the loan request

+ Request
    + Headers
    
            X-transactionId: 123456789

+ Response 201 (application/json)
    + Headers

            X-transactionId: 123456789
            X-test-mode: true
            Location: loan_requests/{request_id}/simulations


## Data Structures

### LoanRequest
+ vendorId: 100456420125 (string, required)
   Your vendor identifier.
+ project (Project,required)

### Project

+ loan (Loan, required)

### Loan
+ category: 50,251,252 (enum,required)
    the material code
+ amount: 10000 (number,required)
    The amount in cts.
+ term: 28 (number, required)
    The loan term in month.
+ read_only: false (boolean, optional)
    Indicates if the loan object can be modifed.
    
### CustomisationContext
+ product_family: CLASSICAL, REVOLVING (enum, optional)
