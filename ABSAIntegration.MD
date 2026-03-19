# ABSA Bank Integration

# Key Features

## Bank Statement Import

- Functionality:
  - File based import of bank statements in the required formats.
  - Supports both standard and short formats for ABSA and Standard Bank.
- Setup
  - On Bank Account Card page, select the Bank Statement Import Format that relates to your bank account.

## Payment Export

- Functionality:
  - Exports payment journal data in bank-specific formats.
- Setup:
  - On Bank Account Card page, select the Payment Export Format that relates to your bank account.

## API Integration

Not currently supported for Cloud, available for On Prem.

## Configuration

### Bank Account Card

![alt text](<Absa Bank card.png>)

### API Integration

![alt text](<API integration.png>)

- The Bank API Integration Type must be setup as ABSA
- The Transaction Company Reference Prefix must be setup to populate the Transaction reference numbers on the Payment journal for submission.
- The Other fields are all related to the ABSA environment for the correct connectivity and processing. 

### Vendor Bank Account

![alt text](<Vendor Bank.png>)

### Vendor Card

![alt text](<Vendor Card.png>)

  - Under the Address & Contact information the Our Account No. must be populated with the reference number of the Vendor which will reflect on the Bank Statement. 
  
  ![alt text](<Vendor Card 2.png>)

  - Under the Payments information the Preferred Bank Account Code must be populated.
 
### Payment Journals

*	Payment Batch setup
If more than one Batch will be used for the ABSA integration the No series must be unique for each batch.

![alt text](<Payment Batch.png>)

* Suggest Payments/Creating Journal entries
- Create Payment journal entries.	 

![alt text](<Create Journal Entries.png>)

- The Suggest Vendor Payment can be used or the entries can be captured manually in the journal. 

![alt text](<Payment Journal.png>)

- When populating the journal the system will populate the External Document number and Payment reference, using the Transaction Company Reference Prefix  from the bank account setup as a prefix. Adding a combination of the payment date and incrementing the last number to keep the payment reference/External document number unique. 
- The integration does not allow duplicate External document numbers. 
- Our Account No is populated on the payment journal and can be modified if need be. 
- The Bank API – Correlation ID and Bank API – Response info will be populated on submission to the bank.

![alt text](<Payment Journal 2.png>)

The Payment Method code will be populated on submission. 

###	Submission

#### Approvals
- Before the batch can be submitted to the bank the journal batch must be approved.
- A workflow must be setup. 

![alt text](<Event Conditions Approval of Batch.png>)

![alt text](<Payment Journal Submit to Bank.png>)

![alt text](<Approval Error.png>)

![alt text](<Approval Confirmation.png>)

#### Submission to Bank

After approval the Journal can be submitted to the bank.
 
![alt text](<Journal after approval.png>) 

- The Bank Submission Status will show “Submit to Bank”
- The Bank-API – Correlationid and Bank API – Response info will be populated. 
- The Bank-API – Correlationid is the unique id the Bank uses to ensure there are no duplicate payments made to the Vendor. 
- In example above the Payment status show as Pending.
- The Payment status values:
  - Paid – If the submission was successfully submitted and paid on the ABSA system. 
  - Rejected – This can be due to a duplicate payment amount for the same vendor bank on the same day, duplicate payment reference or invalid bank account.
  - Pending – Pending is queuing the payment the ABSA site.
  - On requesting Manual Query Payment status the system will check if the pending request was submitted successfully and change the Payment status to Paid.
  
![alt text](<Manual Query Payment Status.png>)

#### Posting
- Only lines which are status Paid will be posted.
- As example below , another payment was entered with the same amount and the status changed to rejected. When posting the batch only the second line will be posted.

![alt text](<Payments after posting.png>)

- Rejected lines on the batch can be deleted.
- When status is pending/paid no changes to the batch are allowed.
- To reopen the batch the Un-submit to Bank function must be selected. 

#### Job Queue
The Journal posting can be setup in a Job queue which will re-check the payment status to the Bank for pending and will automatically post the lines on the Batch marked as paid. 
