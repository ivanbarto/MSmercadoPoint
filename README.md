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
