
FORMAT: 1A
HOST: http://polls.apiblueprint.org/

# loan-application API

Loan application is a simple API allowing consumers to subscribe a loan.

![alt text](https://github.com/willy77/loan-api/blob/master/model.jpg?raw=true)

To create a Loan follow the following process:

 1. [Create a loan request](#create_loan_request)
 2. [Ask for simulation](#create_loan_simulation)
 3. [Retreive simulation result](#read_simulation_result).

In the document, the following convention apply:

 - All amounts are in cts.
 - All rates are multiplied by 10000

Each request allows you to add the following headers:
- The `X-transactionId` header allows you to send your transaction id, in order to help us when debuging.

## Data Structures

### LoanRequest
+ vendorId: 100456420125 (string, required)
   Your vendor identifier.
+ project (Project,required)

### Project

+ personal_financing (PersonnalFinancing, required)

### PersonnalFinancing
+ category: 50,251,252 (enum,required)
    the material code
+ amount: 3000000 (number,required)
    The amount in cts.
+ term: 20 (number, required)
    The loan term in month.
+ read_only: false (boolean, optional)
    Indicates if the loan object can be modifed.
    
### CustomisationContext

+ product_family: CLASSICAL, REVOLVING (enum, optional)
+ engagement: NONE, SCORED, FINAL (enum,optional)

### SimulationGroup

+ rank: 10 (number)
+ kind: result, sample (enum)
+ simulations (array[Simulation])

### Simulation

+ id: 01
+ type: main,secondary,alternative (enum)
  When several simulation are present in a group, they can play different roles.
+ rating: LOW,HIGH,FIXED (enum,optional)
+ proposal (enum)
    + (ClassicalFinancing)
    + (RevolvingFinancing)

### AbstractLoanProposal
+ term: 20 (number, required)
+ requested_amount: 3000000 (number,required)
+ rate (RATE)
+ TAEG (RATE)
+ insurance_included: false (boolean)
+ total_amount: 3070320 (number, required)
+ interest: 26940 (number)
+ insurance (Insurance)
+ loan_cost: 70320 (number,required)

### ClassicalFinancing (AbstractLoanProposal)
+ monthly_payment: 153516 (number,required)
+ fees: 0 (number)

### RevolvingFinancing (AbstractLoanProposal)
+ maxterm: 24 (number, required)
+ installments (array[Installment],required)


### RATE
+ kind: fixed,variable (enum,required)
+ value: 26900 (number, required)

### Insurance

+ rating: LOW,HIGH,FIXED (enum,optional)
+ amount: 3761 (number)
+ total_amount: 75220 (number)
+ TAEA: 29100 (number)

### Installment
+ number: 19 (number, required)
+ amount:  11400  (number, required)
