<!-- loiod5660c146a93483692335e9d79a8c58f -->

# Configure the AMQP Receiver Adapter

You se the Advanced Message Queuing Protocol \(AMQP\) receiver adapter to send messages from Cloud Integration to queues or topics in an external message broker.



> ### Note:  
> In the following cases certain features might not be available for your current integration flow:
> 
> -   You are using a product profile other than the one expected \(see [Updating your Existing Integration Flow](updating-your-existing-integration-flow-1f9e879.md)\).
> 
> -   A feature for a particular adapter or step was released after you created the corresponding shape in your integration flow \(see [Product Profiles](product-profiles-8007daa.md)\). To use the latest version of a flow step or adapter, edit your integration flow, delete the flow step or adapter, add the step or adapter, and configure the same. Finally, redeploy the integraion flow.

> ### Note:  
> To be able to connect to queues or topics, you have to create queues and/or topics in the message broker. This needs to be done in the message broker with the configuration tools provided by the message broker.

> ### Note:  
> Queues, topics, and messages can only be monitored using tools provided by the message broker. Those monitors are not integrated into SAP Integration Suite . In SAP Integration Suite , the integration flows using the AMQP adapter are monitored and the messages send to or consumed from the message broker.

> ### Note:  
> This adapter exchanges data with a remote component that might be outside the scope of SAP. Make sure that the data exchange complies with your company’s policies.



Once you have created a receiver channel and selected the AMQP receiver adapter \(TCP or WebSocket\), you can configure the following attributes. See [Overview of Integration Flow Editor](overview-of-integration-flow-editor-db10beb.md).



The following values are displayed in the *General* tab after a channel has been established. To change the configurations, you need to configure a new channel.

<a name="loiod5660c146a93483692335e9d79a8c58f__table_nbt_4sw_jjb"/>General


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

 *Name/Adapter Type* 



</td>
<td valign="top">

AMQP



</td>
</tr>
<tr>
<td valign="top">

 *Transport Protocol* 



</td>
<td valign="top">

The protocol that the message broker supports:

-   *TCP*

-   *WebSocket*




</td>
</tr>
<tr>
<td valign="top">

 *Message Protocol* 



</td>
<td valign="top">

 *AMQP 1.0* 



</td>
</tr>
</table>

Select the *Connection* tab and provide values in the fields as follows.

<a name="loiod5660c146a93483692335e9d79a8c58f__table_j3m_1vw_jjb"/>Connection


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

 *Host* 



</td>
<td valign="top">

Specify the hostname of the message broker.



</td>
</tr>
<tr>
<td valign="top">

 *Port* 



</td>
<td valign="top">

Specify the port of the message broker.



</td>
</tr>
<tr>
<td valign="top">

 *Proxy Type* 



</td>
<td valign="top">

The type of proxy that you’re using to connect to the target system.

Select *Internet* if you’re connecting directly to the message broker.

Select *On-Premise* if you’re connecting to an on-premise message broker.

For more information, see [Using SAP Cloud Connector with Cloud Integration Adapters](../40-RemoteSystems/using-sap-cloud-connector-with-cloud-integration-adapters-65a60e7.md).



</td>
</tr>
<tr>
<td valign="top">

 *Path* \(only if *WebSocket* is selected as the *Transport Protocol* in the *General* tab\)



</td>
<td valign="top">

Specify the access path of the message broker.



</td>
</tr>
<tr>
<td valign="top">

 *Connect with TLS* 



</td>
<td valign="top">

Select if *TLS* has to be used for the connection.



</td>
</tr>
<tr>
<td valign="top">

*Location ID* \(only if *On-Premise* is selected for *Proxy Type*\)



</td>
<td valign="top">

To connect to an SAP Cloud Connector instance associated with your account, enter the location ID that you defined for this instance in the destination configuration on the cloud side.



</td>
</tr>
<tr>
<td valign="top">

 *Authentication* 



</td>
<td valign="top">

Select the authentication method the message broker supports. *SASL* is selected by default.

-   *SASL*

-   *OAuth2 Client Credentials*

-   *None*


> ### Note:  
> Option *OAuth2 Client Credentials* is only available for WebSocket.



</td>
</tr>
<tr>
<td valign="top">

 *Credential Name* \(only if *SASL* or *OAuth2 Client Credentials* is selected for *Authentication*\)



</td>
<td valign="top">

Specify the alias of the deployed credentials.



</td>
</tr>
</table>

Select the *Processing* tab and provide values in the fields as follows.

<a name="loiod5660c146a93483692335e9d79a8c58f__table_hv2_lql_kjb"/>Processing


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

 *Destination Type* 



</td>
<td valign="top">

Specify if messages should be sent to queues or topics in the message broker.



</td>
</tr>
<tr>
<td valign="top">

 *Destination Name* 



</td>
<td valign="top">

Enter the name of the queue or topic.

This value can be defined dynamically by using the following expressions: `${header.queueabc}` or `${property.queueabc}`.



</td>
</tr>
<tr>
<td valign="top">

 *Expiration Period \(in s\)* 



</td>
<td valign="top">

Specify the Time to Live \(TTL\) for the message. If nothing is specified, the setting for the queue or topic subscription in the message broker applies.



</td>
</tr>
<tr>
<td valign="top">

 *Delivery* 



</td>
<td valign="top">

Specify whether the message broker has to make sure that the message is not lost, even in case of unexpected terminations.

-   *Persistent*

-   *Non-Persistent*




</td>
</tr>
<tr>
<td valign="top">

 *Message Type* 



</td>
<td valign="top">

Define the message type to be used for sending the message to the message broker. Choose between the following options:

-   *Automatic* \(recommended\): In this case, the adapter sets the message type based on the message format before the receiver channel.

-   *Binary*: In this case, the adapter converts the message into a binary message before sending.

-   *Text*: In this case, the adapter converts the message into a string before sending.


> ### Note:  
> Select *Binary* or *Text* only if your application receiving the message requires a specific message type.
> 
> Also, if you select *Binary* or *Text*, you can define the character encoding with the help of `CamelCharsetName` \(either header or property\) in the *Content Modifier*. In case you don't set the `CamelCharsetName` header or property, the transformation will use UTF-8 character encoding. See [Content Modifier Basics](content-modifier-basics-b0576a8.md) and [About Headers and Exchange Properties](about-headers-and-exchange-properties-0974c4f.md).



</td>
</tr>
<tr>
<td valign="top">

 *Header Format Handling* 



</td>
<td valign="top">

There are two options for forwarding the message header name:

-   *Passthrough* \(default option\):

    Choose this option to pass the message header without transformation. For example, message-header.1 is forwarded as message-header.1.

-   *Replace*:

    Choose this option to replace dots and hyphens of a message header with \_HYPHEN\_ and \_DOT\_. For example, message-header.1 is forwarded as message\_HYPHEN\_header\_DOT\_1.




</td>
</tr>
</table>

**Related Information**  


[Blog: Cloud Integration – Connecting to Messaging Systems using the AMQP Adapter](https://blogs.sap.com/2019/11/20/cloud-integration-connecting-to-external-messaging-systems-using-the-amqp-adapter/)

[Blog: Cloud Integration – How to Connect to an On-Premise AMQP server via Cloud Connector](https://blogs.sap.com/2020/01/17/cloud-integration-how-to-connect-to-an-on-premise-amqp-server-via-cloud-connector/)

