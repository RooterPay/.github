# Rooter
## TL;DR
Rooter is a payment terminal that supports both fiat and crypto payments out of the box, hiding the technicalities from the merchant and the user. The user can tap their card as usual and the payment will be processed according to the best route available, the card schema (Visa/Mastercard/Amex) or via stables on the blockchain.

## Repositories
* [firmware]() the payment terminal app that processes card data in a PCI-DSS compliant way and, if it detects a crypto card using the card BIN number, routes the transaction to the issuer backend directly.
* [example card backend]() a mock of crypto card backends, that signs a transaction with the user session key saved inside the ISO8583 optional fields of the IC card.
* [landing]() the project landing page in NextJS rendered statically using a GitHub action
* [backend]() the cloudPOS backend for stock management and financial analytics

## How it works
When the user presents a card to the payment terminal, the firmware Android app will check if the *Bank Identification Number* corresponds to a crypto card (for instance Holyheld, Gnosis Pay, Rain or Metamask card).
If not, the payment is routed to the payment schema - Visa/Mastercard/Amex.
If yes, the session key saved in the card is extracted and relayed to the issuer backend to sign a direct transfer from the user to the merchant in a P2P way: doing so we can skip the card schema, the payment acquirer and other intermediaries and save about 85% of the transaction costs.
