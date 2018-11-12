## Cybersource Reason Codes (GW01)

| Reason Code | Description                              |
| ----------- | ---------------------------------------- |
| 100         | Successful transaction. If ccAuthReply_processorResponse is 08, you can accept the transaction if the customer provides you with identification. |
| 101         | The request is missing one or more required fields. Possible action: see the reply fields missingField_0 through missingField_N for which fields are missing. Resend the request with the complete information. For information about missing or invalid fields. |
| 102         | One or more fields in the request contains invalid data. Possible action: see the reply fields invalidField_0 through invalidField_N for which fields are invalid. Resend the request with the correct information. For information about missing or invalid fields. |
| 104         | The merchant reference code for this authorization request matches the merchant reference code of another authorization request that you sent within the past 15 minutes. Possible action: Resend the request with a unique merchant reference code. |
| 110         | Only a partial amount was approved.      |
| 150         | General system failure. See the documentation for your CyberSource client for information about handling retries in the case of system errors. |
| 151         | The request was received but there was a server timeout. This error does not include timeouts between the client and the server. Possible action: To avoid duplicating the transaction, do not resend the request until you have reviewed the transaction status in the Business Center. |
| 152         | The request was received, but a service did not finish running in time. Possible action: To avoid duplicating the transaction, do not resend the request until you have reviewed the transaction status in the Business Center. |
| 200         | The authorization request was approved by the issuing bank but declined by CyberSource because it did not pass the Address Verification System (AVS) check. Possible action: You can capture the authorization, but consider reviewing the order for the possibility of fraud. |
| 201         | The issuing bank has questions about the request. You do not receive an authorization code programmatically, but you might receive one verbally by calling the processor. Possible action: Call your processor to possibly receive a verbal authorization. For contact phone numbers, refer to your merchant bank information. |
| 202         | Expired card. You might also receive this value if the expiration date you provided does not match the date the issuing bank has on file. Possible action: Request a different card or other form of payment. |
| 203         | General decline of the card. No other information was provided by the issuing bank. Possible action: Request a different card or other form of payment. |
| 204         | Insufficient funds in the account. Possible action: Request a different card or other form of payment. |
| 205         | Stolen or lost card. Possible action: Review this transaction manually to ensure that you submitted the correct information. |
| 207         | Issuing bank unavailable. Possible action: Wait a few minutes and resend the request. |
| 208         | Inactive card or card not authorized for card-not-present transactions. Possible action: Request a different card or other form of payment. |
| 209         | CVN did not match. Possible action: Request a different card or other form of payment. |
| 210         | The card has reached the credit limit.Possible action: Request a different card or other form of payment. |
| 211         | Invalid CVN. Possible action: Request a different card or other form of payment. |
| 221         | The customer matched an entry on the processor’s negative file. Possible action: Review the order and contact the payment processor. |
| 230         | The authorization request was approved by the issuing bank but declined by CyberSource because it did not pass the CVN check. Possible action: You can capture the authorization, but consider reviewing the order for the possibility of fraud. |
| 231         | Invalid account number. Possible action: Request a different card or other form of payment. |
| 232         | The card type is not accepted by the payment processor. Possible action: Contact your merchant bank to confirm that your account is set up to receive the card in question. |
| 233         | General decline by the processor. Possible action: Request a different card or other form of payment. |
| 234         | There is a problem with the information in your CyberSource account. Possible action: Do not resend the request. |
| 235         | The requested capture amount exceeds the originally authorized amount. Possible action: Issue a new authorization and capture request for the new amount. |
| 236         | Processor failure. Possible action: Wait a few minutes and resend the request. |
| 237         | The authorization has already been reversed. Possible action: No action required. |
| 238         | The authorization has already been captured. Possible action: No action required. |
| 239         | The requested transaction amount must match the previous transaction amount. Possible action: Correct the amount and resend the request. |
| 240         | The card type sent is invalid or does not correlate with the credit card number. Possible action: Confirm that the card type correlates with the credit card number specified in the request, then resend the request. |
| 241         | The request ID is invalid. Possible action: Request a new authorization, and if successful, proceed with the capture. |
| 242         | You requested a capture, but there is no corresponding, unused authorization record. Occurs if there was not a previously successful authorization request or if the previously successful authorization has already been used by another capture request. Possible action: Request a new authorization, and if successful, proceed with the capture. |
| 243         | The transaction has already been settled or reversed. Possible action: No action required. |
| 246         | One of the following: The capture or credit is not voidable because the capture or credit information has already been submitted to your processor. You requested a void for a type of transaction that cannot be voided. Possible action: No action required. |
| 247         | You requested a credit for a capture that was previously voided. Possible action: No action required. |
| 250         | The request was received, but there was a timeout at the payment processor. Possible action: To avoid duplicating the transaction, do not resend the request until you have reviewed the transaction status in the Business Center. |
| 254         | Stand-alone credits are not allowed. Possible action: Submit a follow-on credit by including a request ID in the credit request. A follow-on credit must be requested within 60 days of the authorization. To process stand-alone credits, contact your CyberSource account representative to find out if your processor supports stand-alone credits. |
| 400         | Soft Decline - Fraud score exceeds threshold. Possible action: You can capture the authorization, but consider reviewing the order for the possibility of fraud. |
| 450         | Apartment number missing or not found. Possible action: Ask the customer to verify the address information and resend the request. |
| 451         | Insufficient address information. Possible action: Ask the customer to verify the address information and resend the request. |
| 452         | House/Box number not found on street. Possible action: Ask the customer to verify the address information and resend the request. |
| 453         | Multiple address matches were found. Possible action: Ask the customer to verify the address information and resend the request. |
| 454         | P.O. Box identifier not found or out of range. Possible action: Ask the customer to verify the address information and resend the request. |
| 455         | Route service identifier not found or out of range. Possible action: Ask the customer to verify the address information and resend the request. |
| 456         | Street name not found in Postal code. Possible action: Ask the customer to verify the address information and resend the request. |
| 457         | Postal code not found in database. Possible action: Ask the customer to verify the address information and resend the request. |
| 458        | Unable to verify or correct address. Possible action: Ask the customer to verify the address information and resend the request. |
| 459        | Multiple addres matches were found (international). Possible action: Ask the customer to verify the address information and resend the request. |
| 460        | Address match not found (no reason given). Possible action: Ask the customer to verify the address information and resend the request. |
| 461        | Unsupported character set. Possible action: Verify the character set that you are using to process transactions. |
| 475        | The cardholder is enrolled in Payer Authentication. Possible action:Please authenticate the cardholder before continuing with the transaction. |
| 476        | Encountered a Payer Authentication problem. Payer could not be authenticated. |
| 480        | The order is marked for review by Decision Manager. |
| 481        | The order has been rejected by Decision Manager. |
| 520        | Soft Decline - The authorization request was approved by the issuing bank but declined by CyberSource based on your Smart Authorization settings |
| 700        | The customer matched the Denied Parties List. Possible action: Reject the customer's order.|
| 701        | Export bill_country/ship_country match. Possible action: Reject the customer's order.|
| 702        | Export email_country match. Possible action: Reject the customer's order.|
| 703        | Export hostname_country/ip_country match. Possible action: Reject the customer's order.|


> Información tomada de: https://support.cybersource.com/cybskb/index?page=content&id=C1401&actp=search&viewlocale=en_US&searchid=1516825358000
