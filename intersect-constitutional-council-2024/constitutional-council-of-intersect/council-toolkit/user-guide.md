---
icon: square-user
---

# User guide

### To sign a vote with the Council Toolkit , you will need:

* A Chromium Browser.
* A Windows or Apple computer.
* A compatible wallet, controlling a voter key.
  * We currently recommend Lace and Eternl.
* [`council-toolkit.gov.tool`](https://council-toolkit.gov.tools/)

### Instructions

* Toolkit is compatible with two environments : Pre-Prod and Mainnet
* Visit Council Toolkit: [Council Toolkit ](https://council-toolkit.gov.tools/)
* Have a unsigned voting transaction ready (provided by the orchestrator)
* You are ready to produce a witness (a signature) !!

### Step-by-step guide to produce a signature&#x20;

*   Click 'Connect Wallet'&#x20;

    * Establish a connection between the wallet and the toolkit&#x20;

    <figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

    * Make sure you allow wallet to be used by Dapp on wallet's settings
    * Once connection is established, your _**voter key hash**_ and _**wallet network**_ will be displayed.

    <div align="left"><figure><img src="../.gitbook/assets/1 (4).png" alt=""><figcaption></figcaption></figure></div>

    * Upload your unsigned voter transaction (that has been sent by the 'orchestrator') by clicking UPLOAD button.

    <figure><img src="../.gitbook/assets/1 (5).png" alt=""><figcaption></figcaption></figure>

    * Upon selecting the unsigned voter transaction file , the transaction hex will be displayed.

    <figure><img src="../.gitbook/assets/1 (6).png" alt=""><figcaption></figcaption></figure>

    * Validation checks are done by clicking "CHECK TRANSACTION" button .

    <figure><img src="../.gitbook/assets/1 (7).png" alt=""><figcaption></figcaption></figure>

    * A total of 8 validation check are preformed that confirm:
      * you are a required signer.
      * you have an  un-signed transaction, needed to be signed.
      * both the unsigned transaction and the wallet are in the same network.
      * the uploaded transaction is un-signed, in need for a signature(a witness).
      * the vote transaction refers Intersect's ICC credentials.
      * you are signing only one vote in the vote transaction.
      * no certificates are part of the vote transaction.
      * your key is in the Intersect's ICC hierarchy.
      * the metadata document on the hosted at the provided URL , matches the provided hash.
    * Voting details are displayed and the user needs to confirm they are correct before proceeding to sign the vote transaction.

    <figure><img src="../.gitbook/assets/1 (8).png" alt=""><figcaption></figcaption></figure>

    * After confirming the governance action ID you are voting on , the vote choice and the metadata you can proceed with signing the transaction.

    <figure><img src="../.gitbook/assets/1 (1).png" alt=""><figcaption></figcaption></figure>

    <figure><img src="../.gitbook/assets/1 (2).png" alt=""><figcaption></figcaption></figure>

    * Upon clicking on the 'SIGN TRANSACTION" button , your soft wallet is going to request you the spending password in order for the wallet to sign the transaction and create a signature (a witness)
    * Signature(the witness) then will be retrieved by our app where you can download it by clicking "DOWNLOAD" button and ready to send it to the 'orchestrator'

    <figure><img src="../.gitbook/assets/1 (3).png" alt=""><figcaption></figcaption></figure>



