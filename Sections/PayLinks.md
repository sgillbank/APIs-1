PayLinks
========

The PayLinks API is used for creating, updating and retrieving PayLinks. Please note that all requests require API authentication by *Security Token*, see our [guide](https://github.com/ShaunSharples/APIs/blob/ShaunSharples-patch-1/Sections/Authentication.md#security-token) on how to authenticate.

Create a PayLink
----------------

* `POST /api/document` will create and save a PayLink document to the PayLink server based on the request JSON payload

###### Request
<pre>
{
  <b><i>"SetupId": "PFP"</i></b>,
  <b>"Currency": "USD"</b>,
  <b>"Amount": 49.99</b>,
  <b>"DocumentAmount": 49.99</b>,
  "TaxAmount": 0,
  "TradeDiscount": 0,
  "Freight": 0,
  "MiscAmount": 0,
  <b>"CustomerNumber": "John Doe Ltd"</b>,
  "CustomerName": null,
  <b>"IsMultipleInvoice": false</b>,
  "DocumentNumber": null,
  "TransactionType": "Sale",
  <b>"DocDate": "2015-10-28T00:00:00"</b>,
  "DueDate": "2015-10-31T00:00:00",
  "DocType": 0,
  "PaymentTerm": null,
  "SourceOfDocument": 0,
  "BatchSource": 0,
  "BatchNo": null,
  "MerchantEmail": null,
  "ReturnUrl": null,
  "Tax": null,
  "ShippingAddress": null,
  "BillingAddress": null,
  "Items": null,
  "UserDefinedFields": null,
  "PostDataType": "PaymentLine",
  <b><i>"Payment": {
    "CreditCardGateway": "PFP",
    "ECheckGateway": "",
    "AcceptType": 1
  }</i></b>,
  <b>"Notification": {
    "Type": "All"
  }</b>,
  <b>"NotificationEmail": "John.Doe@payfabric.com"</b>,
  <b>"NotificationPhone": "123456789"</b>
}
</pre>

Please note that **bold** fields are required fields, the **Payment** object **or** **SetupId** field must be supplied, and all others are optional. For more information and descriptions on available fields please see our [wiki page](https://github.com/PayLink/APIs/wiki/API-Object#paylink).

###### Response
<pre>
{
  "Id": "h3GSpCZKsEWNxFv6T_y_Gw",
  "TransactionKey": "151028003864"
}
</pre>

The response will include the full document object, see the [Retrieve a PayLink](https://github.com/PayLink/APIs/edit/master/Sections/PayLinks.md#retrieve-a-paylink) endpoint for more information.

Update a PayLink
----------------

* `PATCH /api/document` will update a PayLink document with new information based on the request JSON payload

###### Request
<pre>
{
    "Id": "AdFXqnNNf0GDNwiO5UE_fw"
}
</pre>

Please note that the **Id** field is the only required field for an update. Only the fields that need updating should be included, see the [Create a PayLink](https://github.com/PayLink/APIs/edit/master/Sections/PayLinks.md#create-a-paylink) endpoint for more information.

###### Response
<pre>
{
  "Result": "True"
}
</pre>

Retrieve a PayLink
------------------

* `GET /api/document/AdFXqnNNf0GDNwiO5UE_fw` will return the specified PayLink document

###### Response
<pre>
{
}
</pre>

Retrieve PayLinks
-----------------

* `GET /api/document` will return all PayLink documents created
* `GET /api/document?$filter` will return all PayLink documents based on an OData ([What is OData?](http://www.odata.org/documentation/odata-version-3-0/url-conventions/)) query
 
###### Available OData Fields
>
| Field | Description | 
| :------------- | ------------- | 
| CustomerNumber | The customer number specified during PayLink creation. |
| DocumentNumber | The document number specified during PayLink creation. |
| DocDate | The document date specified during PayLink creation. |
| DueDate | The payment due date specified during PayLink creation. |
| CreatedOn | The date the PayLink was created. |
| PaidOn | The date the PayLink was paid. |
| Amount | The amount of the PayLink. |
| Email | The notification email assigned to the PayLink. |
| Status | The status of the PayLink, available values are `0 = draft, 1 = waiting for payment, 2 = cancelled, 3 = paid, 4 = ERP posting failed, 5 = ERP posting done` |
| TransactionKey | The PayFabric transaction key. |

###### Response
<pre>
{
}
</pre>

Retrieve a PayLink URL
----------------------

* `GET /api/document/retrieve/AdFXqnNNf0GDNwiO5UE_fw/link` will return the specified PayLink documents' unique URL

###### Response
<pre>
{
}
</pre>

Remove a PayLink
----------------

* `DELETE /api/document/AdFXqnNNf0GDNwiO5UE_fw` will remove the specified PayLink document permanently

###### Response
<pre>
{
}
</pre>

Cancel a PayLink
----------------

* `POST /api/document/AdFXqnNNf0GDNwiO5UE_fw/cancel` will cancel a PayLink document

###### Response
<pre>
{
  "Result": "True"
}
</pre>
