# MSmercadoPoint
Microservice created in order to link payments with MercadoPoint

Mercadopago reference: https://www.mercadopago.com.ar/developers/es/docs/mp-point/integration-api/introduction

The main idea that this microservice has is to give an endpoint where link a PDV (punto de venta) with a Point Plus Device (POS), in order to allow the user to manage sales payments with that device and decouple PDV from payments.

This is the Use Case sequence diagram:
![image](https://user-images.githubusercontent.com/66323499/176477365-ebe93b07-1e8b-4b3e-a39e-dea9792f9f39.png)

This microservice acts as the Integrator Server entity.

As a PDV, you must:

1- Create a Payment Intention. To do this, the PDV calls this microservice with the required parameters.

2- Wait for a payment confirmation from this microservice. The PDV has to show a propper UI, giving instructions to procede with the payment and a  indeterminate progress.

There are 3 possible states on the response:

1- APPROVED: the payment was a success
```
{
 "amount": 100,
 "caller_id": 09876543,
 "client_id": 1234567890,
 "created_at": "2021-11-29 17:10:37",
 "id": "abcdef123-8ab5-4139-9aa3-abcd123",
 "payment": {
   "id": 123456789,
   "state": "approved",
   "type": "credit_card"
 },
 "state": "FINISHED",
 "additional_info": {
   "external_reference": "information",
   "ticket_number": "39SHDKKDJ"
 }
}
```

2- CANCELED: the user has cancelled the paymnet process for a particular reason
```
{
 "amount": 100,
 "caller_id": 09876543,
 "client_id": 1234567890,
 "created_at": "2021-11-29 17:10:37",
 "id": "abcdef123-8ab5-4139-9aa3-abcd123",
 "state": "CANCELED",
 "additional_info": {
   "external_reference": "information",
   "ticket_number": "39SHDKKDJ"
 }
}
```

3- ERROR: an error has occured while the user was paying
```
{
 "amount": 100,
 "caller_id": 09876543,
 "client_id": 1234567890,
 "created_at": "2021-11-29 17:10:37",
 "id": "abcdef123-8ab5-4139-9aa3-abcd123",
 "state": "ERROR",
 "additional_info": {
   "external_reference": "information",
   "ticket_number": "39SHDKKDJ"
 }
}
```
