# First National Bank Integration

## Key Features

### Bank Statement Import

- Functionality:
  - File based import of bank statements in the required formats.
  - Supports both standard and short formats for ABSA and Standard Bank.
- Setup
  - On Bank Account Card page, select the Bank Statement Import Format that relates to your bank account.

### Payment Export

- Functionality:
  - Exports payment journal data in bank-specific formats.
- Setup:
  - On Bank Account Card page, select the Payment Export Format that relates to your bank account.

### API Integration for FNB Direct Debit Management

- Automates the creation, processing, and status updates of direct debit collections.
- Supports SEPA-compliant direct debit mandates.
- Only supports direct debit instructions for South African Banks in South African Rand.

## Bank Activation

You need to obtain a Client ID and Client Secret from the bank to use the integration. Contact your company’s bank account manager to obtain these setups and enable your account for the integration.

They will also be able to provide you with Sandbox setups if you want to try it out first.

Add these setups to the Bank Integration Setup page.

If Production Active = No, it will target the bank’s sandbox environment. With Production Active = Yes, it will target bank production environment.

![alt text](./images/image-3.png)

> NOTE: You will not be able to enable it as Production Active in a Sandbox environment.

### Bank Account

| Field | Value | Description |
| --- | --- | --- |
| Bank Branch No. |  | Required |
| Bank Account No. |  | Required |
| Bank Account Type |  | Required |
| SEPA Direct Debit Exp. Format | FNB-DD | During Direct Debit Export, this lets the system know which format to use. The Bank Integration app will then confirm if the selected bank account on the Direct Debit Collection has a Bank Export Format linked and confirm if it is relevant to a specific bank. Each export and their associated checks are therefore only done if appropriate. |
| Direct Debit Msg. Nos. |  | Required |
| Creditor No. |  | This is the company abbreviation used in the export. |
| Service Level |  | Required |
| Batch Booking |  | If Yes, Transactions will be posted to the creditor account in a consolidated manner. A single transaction entry will be posted to the creditor account, for the full value of all transactions. Any transactions that fail will result in a reversal entry being posted on the creditor account. Else, the transactions will be posted to the creditor account in an itemised manner. An entry will be posted into the creditor account for each successful transaction. |
| Auto Post Direct Debit Collection |  | Automatically post the Direct Debit Collection once collections report has been received from the bank and there are no more pending entries. |
| General Journal Template |  | The template to use when automatically posting the direct debit collection |
| General Journal Batch |  | The batch to use when automatically posting the direct debit collection |

![alt text](./images/image-6.png)

### Customer Bank Account

| Field | Value | Description |
| --- | --- | --- |
| Bank Branch No. |  | Required |
| Bank Account No. |  | Required |
| Bank Account Type |  | Required |
| Service Level |  | Required |
| Max Invoices on Direct Debit |  | Indicates the maximum number of invoices that can be loaded on a Direct Debit Collection |
| SWIFT Code |  | Required |

>NOTE: **SEPA Direct Debit Mandates**: No changes have been made to this table, just know that an active mandate is required for this > functionality to work.

![alt text](./images/image-7.png)
