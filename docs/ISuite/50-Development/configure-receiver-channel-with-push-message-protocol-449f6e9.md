<!-- loio449f6e94db044b44864a4878c08237d5 -->

# Configure Receiver Channel with Push Message Protocol

Configure the AS4 receiver channel as a sending Message Service Handler \(MSH\) to send business documents.



<a name="loio449f6e94db044b44864a4878c08237d5__prereq_cdl_kdg_tdb"/>

## Prerequisites

-   You must deploy the private key pair in theCloud Integration keystore for signing the AS4 message.

-   You must have configured an integration flow in the editor. For more information, see [Overview of Integration Flow Editor](overview-of-integration-flow-editor-db10beb.md).




## Context

Use the *ebMS3 Push* message protocol to transmit AS4 message.

> ### Note:  
> In the following cases certain features might not be available for your current integration flow:
> 
> -   You are using a product profile other than the one expected \(see [Updating your Existing Integration Flow](updating-your-existing-integration-flow-1f9e879.md)\).
> 
> -   A feature for a particular adapter or step was released after you created the corresponding shape in your integration flow \(see [Product Profiles](product-profiles-8007daa.md)\). To use the latest version of a flow step or adapter, edit your integration flow, delete the flow step or adapter, add the step or adapter, and configure the same. Finally, redeploy the integraion flow.

> ### Note:  
> This adapter exchanges data with a remote component that might be outside the scope of SAP. Make sure that the data exchange complies with your company’s policies.



### Connection

Select the *Connection*tab and provide values in the fields as follows.

<a name="loio449f6e94db044b44864a4878c08237d5__table_hmh_hsk_zdb"/>Configure the Connection Details of the Receiving MSH


<table>
<tr>
<th valign="top">

Parameter



</th>
<th valign="top">

Description



</th>
</tr>
<tr>
<td valign="top">

 *Address* 



</td>
<td valign="top">

Define the endpoint URL of the receiving MSH.



</td>
</tr>
<tr>
<td valign="top">

 *Agreement* 



</td>
<td valign="top">

Define the type of the message exchange pattern as agreed between the MSHs for a specific type of business transaction.



</td>
</tr>
<tr>
<td valign="top">

 *Authentication Type* 



</td>
<td valign="top">

Select the authentication type to process the outbound message:

-   *None*

-   *Basic Authentication*

-   *Client Certificate*

-   *SAML Authentication*


You can also set the value of this attribute dynamically using the header ***SAP\_AS4\_Outbound\_Authentication\_Type***.

The valid values are:

-   ***saml***

-   ***basic***

-   ***clientCert***

-   ***none***




</td>
</tr>
<tr>
<td valign="top">

 *SAML Endpoint URL* 



</td>
<td valign="top">

Provide the specific endpoint URL to support SAML-based authentication that allows access to the sending MSH.



</td>
</tr>
<tr>
<td valign="top">

 *Private Key Alias* 



</td>
<td valign="top">

Determine the private key alias for SAML authentication.



</td>
</tr>
<tr>
<td valign="top">

 *Timeout \(in sec.\)* 



</td>
<td valign="top">

Provide a connection timeout period \(in seconds\) to define how long the receiving MSH waits for the AS4 message to be received by the sending MSH.



</td>
</tr>
<tr>
<td valign="top">

*Compress Message*



</td>
<td valign="top">

Enable if you want to compress the message.



</td>
</tr>
</table>

Select the *Processing*tab and provide values in the fields as follows.

<a name="loio449f6e94db044b44864a4878c08237d5__table_ksp_3qg_mdb"/>Processing


<table>
<tr>
<th valign="top">

Parameter



</th>
<th valign="top">

Description



</th>
</tr>
<tr>
<td valign="top">

 *Initiator Party: Party ID* 



</td>
<td valign="top">

Define the ID of the sending MSH.



</td>
</tr>
<tr>
<td valign="top">

 *Initiator Party: Party Type* 



</td>
<td valign="top">

Provide the type of the sending MSH. For example: ***http://abr.gov.au/PartyIdType/ABN*** 



</td>
</tr>
<tr>
<td valign="top">

 *Initiator Party: Role* 



</td>
<td valign="top">

Define the role of the sending MSH. For example: ***http://sbr.gov.au/ato/Role/Business*** 



</td>
</tr>
<tr>
<td valign="top">

 *Responder Party: Party ID* 



</td>
<td valign="top">

Define the ID of the receiving MSH.



</td>
</tr>
<tr>
<td valign="top">

 *Responder Party: Party Type* 



</td>
<td valign="top">

Provide the type of the receiving MSH. For example: ***http://abr.gov.au/PartyIdType/ABN*** 



</td>
</tr>
<tr>
<td valign="top">

 *Responder Party: Role* 



</td>
<td valign="top">

Define the role of the receiving MSH. For example: ***http://sbr.gov.au/agency*** 



</td>
</tr>
<tr>
<td valign="top">

 *Message Partition Channel* 



</td>
<td valign="top">

Specify the partner channel details to enable the partitioned transfer of AS4 messages between AS4 exchange partners.



</td>
</tr>
<tr>
<td valign="top">

 *Service* 



</td>
<td valign="top">

Define the business service of the recipient. For example, payment details of employees for a specific year: ***http://sbr.gov.au/ato/payevnt/2017*** 



</td>
</tr>
<tr>
<td valign="top">

 *Service Type* 



</td>
<td valign="top">

Define the type of service from the recipient.



</td>
</tr>
<tr>
<td valign="top">

 *Action* 



</td>
<td valign="top">

Define the type of action that the user message is intended to invoke. For example: ***Submit.002.00*** 



</td>
</tr>
<tr>
<td valign="top">

 *Attachment Name* 



</td>
<td valign="top">

Define the name for the payload attached to the AS4 message.



</td>
</tr>
<tr>
<td valign="top">

 *Additional Properties* 



</td>
<td valign="top">

Specify the Key, Kype, and Value attributes to modify an existing parameter in the property sheet. For example, if you want to modify the MSH details, you must define a key and its value. The *Type* attribute is used in AS4 message in order to identify the payload.



</td>
</tr>
<tr>
<td valign="top">

*Payload Properties*



</td>
<td valign="top">

Define a key and value to modify the payload attached to AS4 message.



</td>
</tr>
</table>

Select the *Security* tab and provide values in the fields as follows.

<a name="loio449f6e94db044b44864a4878c08237d5__table_vx4_lyg_mdb"/>Security


<table>
<tr>
<th valign="top">

Parameter



</th>
<th valign="top">

Description



</th>
</tr>
<tr>
<td valign="top">

 *WS-Security Type* 



</td>
<td valign="top">

Ensures security implemented in web services for SOAP based messages.



</td>
</tr>
<tr>
<td valign="top">

 *Sign and Enrypt Message* 



</td>
<td valign="top">

Used to sign and encrypt the payload.

You can also set the value of this attribute dynamically by using the header ***SAP\_AS4\_Outbound\_Security\_Type***.

The valid values are:

-   ***sign***

-   ***signAndEncrypt***

-   ***none***




</td>
</tr>
<tr>
<td valign="top">

 *Sign Message* 



</td>
<td valign="top">

Ensures that the outgoing AS4 message is signed.

You can also set the value of this attribute dynamically by using the header ***SAP\_AS4\_Outbound\_Sign\_Message***.

The valid values are:

-   ***true***

-   ***false***




</td>
</tr>
<tr>
<td valign="top">

 *Private Key Alias for Signing* 



</td>
<td valign="top">

Specify an alias for the tenant private key that is to be used to sign the message. The tenant private key is used to sign the request message \(that is sent to the WS provider \(receiver\)\). The tenant private key has to be part of the tenant keystore.



</td>
</tr>
<tr>
<td valign="top">

 *Signature Algorithm* 



</td>
<td valign="top">

Use the relevant algorithm to sign the AS4 message.

You can also set the value of this attribute dynamically by using the header ***SAP\_AS4\_Outbound\_Signing\_Algorithm***.

The valid values are:

-   *SHA256/RSA*

-   *SHA384/RSA*

-   *SHA512/RSA*




</td>
</tr>
<tr>
<td valign="top">

*Public Key Alias for Encryption*

\(only if you select *Sign and Encrypt Message*\)



</td>
<td valign="top">

Specify an alias for the public key that is to be used to encrypt the message.

The receiver \(WS provider\) public key is used to encrypt the request message \(that is sent to the receiver\). This key has to be part of the tenant keystore.

You can also set the value of this attribute dynamically by using the header ***SAP\_AS4\_Outbound\_Encryption\_Cert***. Use this header to set the certificate value to X509 certificate object.



</td>
</tr>
<tr>
<td valign="top">

*Encryption Algorithm*

\(only if you enable *Sign and Encrypt Message*\)



</td>
<td valign="top">

Specify a encryption algorithm to be applied when encrypting the message.

You can also set the value of this attribute dynamically using the header ***SAP\_AS4\_Outbound\_Encryption\_Algorithm***.

The valid values are:

-   *3DES*

-   *AES128*

-   *AES256*




</td>
</tr>
</table>

Select the *Receipt* tab and provide values in the fields as follows.

<a name="loio449f6e94db044b44864a4878c08237d5__table_uhm_wd4_zjb"/>Receipt


<table>
<tr>
<th valign="top">

Parameter



</th>
<th valign="top">

Description



</th>
</tr>
<tr>
<td valign="top">

 *Save Incoming Receipt* 



</td>
<td valign="top">

Saves incoming receipt in the *Message Store* for 90 days. You can refer these receipts for auditing purposes.

You can also set the value of this attribute dynamically using the header ***SAP\_AS4\_Outbound\_Save\_Receipt***.

The valid values are:

-   ***true***

-   ***false***




</td>
</tr>
<tr>
<td valign="top">

 *Verify Receipt Signature* 



</td>
<td valign="top">

Verifies the incoming receipt signature against the public key alias.

You can also set the value of this attribute dynamically using the header ***SAP\_AS4\_Outbound\_Verify\_Receipt***.

-   ***true***

-   ***false***


> ### Note:  
> You can use the ***SAP\_AS4\_Outbound\_Verify\_Receipt\_Cert*** header to set the certificate value to X509 certificate object.



</td>
</tr>
<tr>
<td valign="top">

 *Public Key Alias* 



</td>
<td valign="top">

Enter an alias name to select a public key and corresponding certificate.



</td>
</tr>
</table>

> ### Note:  
> Set the value, provided by ATO, to the ***SAP\_AS4\_Outbound\_ATO\_SAML\_AppliesTo*** header for *AppliesTo* parameter to fetch SAML token from Vanguard.

**Related Information**  


[Externalize Parameters of an Integration Flow](externalize-parameters-of-an-integration-flow-45b2a07.md "")

