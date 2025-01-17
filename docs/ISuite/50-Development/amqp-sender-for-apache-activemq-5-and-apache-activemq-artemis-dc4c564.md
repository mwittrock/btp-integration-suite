<!-- loiodc4c564531494543bbce9fbd4ad18182 -->

# AMQP Sender for Apache ActiveMQ 5 and Apache ActiveMQ Artemis

Enables SAP Integration Suite to consume messages from queues or topic subscriptions in Apache ActiveMQ 5 / Apache ActiveMQ Artemis.



> ### Note:  
> In the following cases certain features might not be available for your current integration flow:
> 
> -   You are using a product profile other than the one expected \(see [Updating your Existing Integration Flow](updating-your-existing-integration-flow-1f9e879.md)\).
> 
> -   A feature for a particular adapter or step was released after you created the corresponding shape in your integration flow \(see [Product Profiles](product-profiles-8007daa.md)\). To use the latest version of a flow step or adapter, edit your integration flow, delete the flow step or adapter, add the step or adapter, and configure the same. Finally, redeploy the integraion flow.

> ### Note:  
> Queues, topics, and messages can only be monitored by using tools provided by the message broker provider. Those monitors are not integrated into SAP Integration Suite . In SAP Integration Suite , the integration flows using the AMQP adapter are monitored and the messages are sent to or consumed from the message broker.

> ### Note:  
> To be able to connect to queues or topics, you have to create queues and/or topics in the message broker. This needs to be done in the message broker, with the configuration tools provided by the message broker. In some messaging systems, you need to configure a *Lock Duration* to make sure that the message is not consumed more than once. This timeout must be longer than the expected processing time of the message, otherwise this would lead to duplicate messages.

> ### Note:  
> This adapter exchanges data with a remote component that might be outside the scope of SAP. Make sure that the data exchange complies with your company’s policies.



To connect Cloud Integration to Apache ActiveMQ 5 and Apache ActiveMQ Artemis, make sure to specify the following parameters in the described way:

When creating the channel \(see [Overview of Integration Flow Editor](overview-of-integration-flow-editor-db10beb.md)\), select adapter type *AMQP* \> *TCP*.



The following values are displayed in the *General* tab after a channel has been established. If you want to change the configurations, you need to configure a new channel.

<a name="loiodc4c564531494543bbce9fbd4ad18182__table_nbt_4sw_jjb"/>General


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

*TCP*



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

Select the *Connection* tab and provide values in the fields as follows:

<a name="loiodc4c564531494543bbce9fbd4ad18182__table_j3m_1vw_jjb"/>Connection


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

Select the authentication method supported by the message broker. Make sure that *SASL* is selected \(default setting\).



</td>
</tr>
<tr>
<td valign="top">

 *Credential Name* \(only if *SASL* or *OAuth2 Client Credentials* are selected for *Authentication*\)



</td>
<td valign="top">

Specify the name of the *User Credentials* artifact.



</td>
</tr>
</table>

Select the *Processing* tab and provide values in the fields as follows.

<a name="loiodc4c564531494543bbce9fbd4ad18182__table_kyp_1yw_jjb"/>Processing


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

 *Queue Name* 



</td>
<td valign="top">

Specify the name of the queue or topic subscription to consume from.



</td>
</tr>
<tr>
<td valign="top">

 *Number of Current Processes* 



</td>
<td valign="top">

Specify the number of processes used for parallel message processing. Note, that these processes are started from each worker node.

> ### Note:  
> The maximum number of parallel processes cannot exceed 99. The default is set to 1.



</td>
</tr>
<tr>
<td valign="top">

*Max. Number of Prefechted Messages*



</td>
<td valign="top">

Enter the max. number of messages that may be prefechted by one worker. The allowed value range is 1 to 100.

The prefetch value is the number of messages that the sender adapter fetches in advance from the broker, and then gradually processes. The prefetch reduces the communication overhead and ensures that when a message has been processed, another is already there and is ready for processing.

If the integration flows that are triggered by the AMQP sender adapter run for longer than a few seconds, it makes sense to set a lower prefetch value. In particular, if the integration flow runs for more than a minute, you should consider setting the value to 1. You can expect then a performance deterioration in the two-digit millisecond range, per message. On the other hand, load balancing between several nodes works better even with short backlogs.

If you need to process a large number of messages with the integration flow, and the processing of the individual message only runs for a few milliseconds, it can be useful to increase the prefetch value.

> ### Note:  
> If you increase the value, this can lead to lock timeouts and the load balancing between the nodes deteriorates. In return, you can expect performance gains in the three-digit microsecond range, per message. For example, with a prefetch value of 100, 10000 messages process approximately a second or two faster.



</td>
</tr>
<tr>
<td valign="top">

*Consume Expired Messages*



</td>
<td valign="top">

Select if the adapter is to consume already expired messages.

By default, this option is deactivated.



</td>
</tr>
<tr>
<td valign="top">

 *Max. Number of Retries* 



</td>
<td valign="top">

Define the number of retries to be executed before a different delivery status is sent to the message broker.

> ### Note:  
> The default is set to 0, meaning there are no retries executed and the delivery status you defined for *Delivery Status After Max. Retries* is sent directly to the message broker. The maximum number of retries can't exceed 99. If you do not specify the number of retries, endless retries are executed. In this case, the delivery status you defined for *Delivery Status After Max. Retries* will never be sent.



</td>
</tr>
<tr>
<td valign="top">

 *Delivery Status After Max. Retries* 



</td>
<td valign="top">

Define one delivery status that is to be sent to the message broker after the maximum number of retries. The following options are supported:

-   *REJECTED*.

-   *MODIFIED\_FAILED\_UNDELIVERABLE*


> ### Note:  
> See this [general information on AMQP](http://docs.oasis-open.org/amqp/core/v1.0/amqp-core-complete-v1.0.pdf) on delivery statuses and their meaning.
> 
> See this [blog](https://blogs.sap.com/2019/11/20/cloud-integration-connecting-to-external-messaging-systems-using-the-amqp-adapter/) for a summary of the capabilities supported by the different brokers.



</td>
</tr>
</table>



<a name="loiodc4c564531494543bbce9fbd4ad18182__section_qgb_ccj_wsb"/>

## Further Constraints

Note the following when using the AMQP adapter to connect Cloud Integration to Apache ActiveMQ 5 and Apache ActiveMQ Artemis:

-   You can configure retry by setting the header `JMSRedelivered`.

-   You can also use header `JMSXDeliveryCount`.


See: [Headers and Exchange Properties Provided by the Integration Framework](headers-and-exchange-properties-provided-by-the-integration-framework-d0fcb09.md)

For more information and an example scenario using this option, see the following SAP Community blog: [https://blogs.sap.com/2019/11/20/cloud-integration-connecting-to-external-messaging-systems-using-the-amqp-adapter/](https://blogs.sap.com/2019/11/20/cloud-integration-connecting-to-external-messaging-systems-using-the-amqp-adapter/).

