Shopping Cart

The shopping cart fulfills the purpose of recording the details of a shopper's desired
purchases, much like the trolley or shopping basket used by the customers of a
conventional supermarket. The online catalog provides a comfortable, discreet and
convenient means of selecting goods or even just looking. As the customer looks
at the items on offer, he or she may examine the prices of one or more such items
and choose to place them in the basket. 
By allowing the customer to then review the entire order, selectively remove some 
items from the 'basket' and check out - pay for - the items using a credit card, the online shopping 
cart gives the user complete control of the buying and ordering process, resulting 
in a shopping experience very similar to the mail order catalog.
Through interaction with a merchant banking account, the customer's purchase is
instantly approved, otherwise the order is subject to modification of one or more of 
the name, address, card number, expiry date and card type used by the purchaser.
In accordance with the terms and conditions of sale, the process of fulfillment
of the order then begins.

Architecture:

Split into CatalogService, CartService, OrderService, PaymentService, FulfillmentService, NotificationService.

Event-driven: after PaymentService confirms, an event (order.paid) is published → consumed by FulfillmentService and NotificationService.

APIs (REST-ish):

GET /products, GET /products/{id}

POST /carts/{id}/items

DELETE /carts/{id}/items/{itemId}

POST /checkout (cart → order)

POST /payments

Events:

order.created, order.paid, order.shipped

Payloads in JSON with order_id, user_id, timestamp.

Infra & NFRs:

PostgreSQL or cloud-managed DB with transactional integrity (cart + order + payment).

Caching for product catalog (Redis).

Payment via PCI-compliant third-party gateway (Stripe, Adyen, etc.).

Observability: logs, metrics, distributed tracing.

Horizontal scaling for stateless services (Cart, Catalog, Checkout).
