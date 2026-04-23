# Configuration

# Table of Contents
- [App Activation](#app-activation)
- [Bank Activation](#bank-activation)
- [General Ledger Setup](#general-ledger-setup)
- [Bank Account](#bank-account)
- [Customer Bank Account](#customer-bank-account)

## App Activation

In Business Central, search for and open "Braintree App Licenses"

![alt text](./images/image-1.png)

1. Enter your e-mail address
2. Select the South African Bank Integrations entry
3. Click Request Subscription/Trial License

We will activate an evaluation license and send it to the email address you specified. The mail will contain a license key. Copy that license key then return to the Braintree App Licenses.

![alt text](./images/image-2.png)

1. Select the South African Bank Integrations entry
2. Click Update License Key
3. Enter the key on the page that opens and click Ok. You should get a message that states “Thank you for registering”

## Bank Activation

You need to obtain a Client ID and Client Secret from the bank to use the integration. Contact your company’s bank account manager to obtain these setups and enable your account for the integration.

They will also be able to provide you with Sandbox setups if you want to try it out first.

Add these setups to the Bank Integration Setup page.

If Production Active = No, it will target the bank’s sandbox environment. With Production Active = Yes, it will target bank production environment.

![alt text](./images/image-3.png)

> NOTE: You will not be able to enable it as Production Active in a Sandbox environment.

## General Ledger Setup

| Field | Value | Description |
| --- | --- | --- |
| LCY Code | ZAR | Validation that local currency is South African Rand |
| SEPA Non-Euro Export | Yes | This functionality is built on standard Business Central Direct Debit functionality. Single European Payments Area (SEPA), by default only supports EUR transactions. |
| SEPA Export w/o Bank Acc. Data | Yes | If this field is disabled, Business Central checks that fields, not required for the export, are populated. We can disable those checks by enabling this setting. |

![alt text](./images/image-4.png)

![alt text](./images/image-5.png)

## Bank Account

| Field | Value | Description |
| --- | --- | --- |
| Bank Branch No. |  | Required |
| Bank Account No. |  | Required |
| Bank Account Type |  | Required |
| SEPA Direct Debit Exp. Format | FNB-DD | During Direct Debit Export, this lets the system know which format to use. The Bank Integration app will then confirm if the selected bank account on the Direct Debit Collection has a Bank Export Format linked and confirm if it is relevant to a specific bank. Each export and their associated checks are therefor only done if appropriate. |
| Direct Debit Msg. Nos. |  | Required |
| Creditor No. |  | This is the company abbreviation used in the export. |
| Service Level |  | Required |
| Batch Booking |  | If Yes, Transactions will be posted to the creditor account in a consolidated manner. A single transaction entry will be posted to the creditor account, for the full value of all transactions. Any transactions that fail will result in a reversal entry being posted on the creditor account. Else, the transactions will be posted to the creditor account in an itemised manner. An entry will be posted into the creditor account for each successful transaction. |
| Auto Post Direct Debit Collection |  | Automatically post the Direct Debit Collection once collections report has been received from the bank and there are no more pending entries. |
| General Journal Template |  | The template to use when automatically posting the direct debit collection |
| General Journal Batch |  | The batch to use when automatically posting the direct debit collection |

![alt text](./images/image-6.png)

## Customer Bank Account

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

## Upgrade and Installation Automation

- Automatic Setup:
  - Automatically creates required setups during app installation.
  - Includes predefined mappings for bank-specific processing codeunits and data exchange definitions.
  - User only needs to map the setups to the appropriate bank accounts.
- Upgrade Support:
  - Ensures smooth transitions during app upgrades by updating field mappings and configurations.

# Job Queue

Two jobs are automatically created with status set to On-Hold and must be set to Ready by a user.
- FNB DD-Collections Report BTR: By default, checks daily for updates from the bank for Direct Debit Collections that have been submitted and updates the Direct Debit Collection Entries.
- DD-Get Unpaids Update BTR: Refreshes the Unpaids Worksheet and updates the Direct Debit Collection Entries that have not yet been posted.
  