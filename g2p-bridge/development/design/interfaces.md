---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Interfaces

<figure><img src="../../../.gitbook/assets/Gitbook-G2PB-Tech-Architecture.jpg" alt=""><figcaption><p>openg2p-g2p-bridge - Technical architecture</p></figcaption></figure>

Refer to the Technical architecture. As shown in the figure, all outward APIs towards a Sponsor bank are abstracted through an interface. This interface is in the library project - **openg2p-g2p-bridge-bank-connectors**

There is also an implementation of the interface (openg2p-g2p-bridge-example-bank-connector), that provides a reference implementation. This connector connects to a simulator application. The simulator application (openg2p-g2p-bridge-example-bank-api) simulates a Sponsor bank.

The interface, the connector factory and the example-bank-connector - together are packaged into a separate git repository - <mark style="color:blue;">**openg2p-g2p-bridge-example-bank**</mark>

The interface defines the following APIs

### 1. check\_funds

| Arguments       | Type   |
| --------------- | ------ |
| account\_number | string |
| currency        | string |
| amount          | number |

returns

| attributes             | Type                                          |
| ---------------------- | --------------------------------------------- |
| funds available status | <p>FUNDS_AVAILABLE<br>FUNDS_NOT_AVAILABLE</p> |

### 2. block\_funds

| Arguments       | Description                                                                            |
| --------------- | -------------------------------------------------------------------------------------- |
| account\_number | The program funding account with the sponsor bank                                      |
| currency        | The currency of the funding account                                                    |
| amount          | The total envelope amount - required for complete disbursal in that disbursement cycle |

returns

| Attributes               | Description                            |
| ------------------------ | -------------------------------------- |
| block\_result            | SUCCESS or FAILURE                     |
| block\_error\_code       | Error in case of FAILURE               |
| block\_result\_reference | The block reference in case of SUCCESS |

### 3. initiate\_payment

It will take a collection of the following structure (payment structure)

This API will only acknowledge receipt of a payment instruction. The actual payment will be effected by the bank asynchronously&#x20;

| Arguments                             | Description                                                                                                                                                           |
| ------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| disbursement\_id                      | This is the unique disbursement id - that identifies a single disbursement inside an envelope                                                                         |
| remitting\_account                    | This is the account in the Sponsor bank - from where the funds are remitted to the beneficiaries                                                                      |
| remitting\_account\_currency          | The currency of the funding account                                                                                                                                   |
| payment\_amount                       | The disbursement amount                                                                                                                                               |
| funds\_blocked\_reference\_number     | The block\_reference\_number - that identifies the amount\_block placed in the bank (funds earmarked for this envelope)                                               |
| beneficiary\_id                       | The beneficiary ID that uniquely identifies the beneficiary in that benefit program - this ID should come from the upstream MIS/PBMS systems                          |
| beneficiary\_name                     | The name of the beneficiary                                                                                                                                           |
| beneficiary\_account                  | The account number of the Beneficiary - in the destination financial service provider                                                                                 |
| beneficiary\_account\_currency        | This should ideally be the same as the funding account currency - typically the local currency of the nation                                                          |
| beneficiary\_account\_type            | <p>BANK_ACCOUNT<br>MOBILE_WALLET<br>EMAIL_WALLET</p>                                                                                                                  |
| beneficiary\_bank\_code               | The Bank code (destination bank) in which the beneficiary account is serviced (applicable for BANK\_ACCOUNT)                                                          |
| beneficiary\_branch\_code             | The branch code (of the destination bank) in which the beneficiary account is serviced (applicable for BANK\_ACCOUNT)                                                 |
| beneficiary\_mobile\_wallet\_provider | The code that identifies the service provider for the mobile wallet (applicable for MOBILE\_WALLET)                                                                   |
| beneficiary\_phone\_no                | The mobile number where the beneficiary will be credited (applicable for MOBILE\_WALLET)                                                                              |
| beneficiary\_email                    | The email address where the beneficiary will be credited (applicable for EMAIL\_WALLET)                                                                               |
| beneficiary\_email\_wallet\_provider  | The code that identifies the service provider for the email wallet (applicable for EMAIL\_WALLET)                                                                     |
| disbursement\_narrative               | Any narrative about the disbursement that will help in reconciliation with the account statement of the funding account                                               |
| benefit\_program\_mnemonic            | The program identifier - This can be used as a narrative by the destination bank - so that the beneficiary is able to identify disbursements from the benefit program |
| cycle\_code\_mnemonic                 | The cycle identifier - that can be potentially used as a narrative by the destination bank - useful for the beneficiary to identify disbursement payments             |
| payment\_date                         | The date on which the disbursement needs to be effected                                                                                                               |

returns

| Attribute | Description        |
| --------- | ------------------ |
| response  | SUCCESS or FAILURE |

### 4. retrieve\_disbursement\_id

| Arguments               | Description                                                                                                                                                                                                                     |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| bank\_reference         | <p>This is the reference number of the payment - that has been assigned by the sponsor bank. <br>The part that follows the "//" in field 61</p>                                                                                 |
| customer\_reference     | <p>This is the reference number (unique for every remittance/disbursement) that has been provided by the g2p-bridge application. <br>In our case - it is the disbursement_id<br>The part that precedes the "//" in field 61</p> |
| narratives \[0] to \[5] | The 6 lines of narratives - 0 to 5 - Field 86 of the Account Statement                                                                                                                                                          |

returns

| Attribute        | Description                                                                                                                                                                                                                                                                                                                                                                |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| disbursement\_id | <p>Depending on the sponsor bank - we need to extract this disbursement id from one of the three attributes<br><br>In most cases - it should be the customer_reference - because that is the customer_reference (disbursement_id) <br><br>The interface abstraction exists to take care of those outlier cases - where the sponsor bank has implemented it differently</p> |

### 5. retrieve\_beneficiary\_name

| Arguments               | Description                                                            |
| ----------------------- | ---------------------------------------------------------------------- |
| narratives \[0] to \[5] | The 6 lines of narratives - 0 to 5 - Field 86 of the Account Statement |

returns

| Attribute         | Description                                                                                               |
| ----------------- | --------------------------------------------------------------------------------------------------------- |
| beneficiary\_name | Depending on the sponsor bank - we need to extract the beneficiary name from one of the narratives fields |

### 6. retrieve\_reversal\_reason

| Arguments               | Description                                                            |
| ----------------------- | ---------------------------------------------------------------------- |
| narratives \[0] to \[5] | The 6 lines of narratives - 0 to 5 - Field 86 of the Account Statement |

returns

| Attribute         | Description                                                                                                                                                                                                                                                                          |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| retrieval\_reason | <p>For reversal transactions <br><br>(where the initial debit to the funding account was subsequently reversed - after a transaction was returned from the destination bank with an error)<br><br>the reason for reversal has to be extracted from one of the narratives fields.</p> |

### Bank Connector Factory

This Factory will return a BankConnector Interface

This BankConnector class will implement the BankConnector Interface

The Factory will return the Connector based on the "benefit\_program.sponsor\_bank\_code"

<mark style="color:blue;">def get\_bank\_connector (sponsor\_bank\_code : string) -> BankConnectorInterface</mark>

### Example Bank Connector

The git baseline includes a connector that connects with the Example Bank (a bank simulator application). The Example Bank Connector - implements all the methods specified by the BankInterface&#x20;
