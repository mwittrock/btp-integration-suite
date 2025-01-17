<!-- loioc5c2e38e0c87472e996dfda04920bfc4 -->

<link rel="stylesheet" type="text/css" href="../css/sap-icons.css"/>

# Configure the OData V2 Receiver Adapter

Configure the OData receiver adapter by understanding the adapter parameters.

> ### Note:  
> In the following cases certain features might not be available for your current integration flow:
> 
> -   You are using a product profile other than the one expected \(see [Updating your Existing Integration Flow](updating-your-existing-integration-flow-1f9e879.md)\).
> 
> -   A feature for a particular adapter or step was released after you created the corresponding shape in your integration flow \(see [Product Profiles](product-profiles-8007daa.md)\). To use the latest version of a flow step or adapter, edit your integration flow, delete the flow step or adapter, add the step or adapter, and configure the same. Finally, redeploy the integraion flow.

> ### Note:  
> This adapter exchanges data with a remote component that might be outside the scope of SAP. Make sure that the data exchange complies with your company’s policies.

OData receiver adapter supports externalization. To externalize the parameters of this adapter, choose *Externalize* and follow the steps mentioned in [Externalize Parameters of an Integration Flow](externalize-parameters-of-an-integration-flow-45b2a07.md).

> ### Note:  
> -   OData adapter doesn’t support ***$format*** and ***$inlineCount*** in query options.
> 
> -   OData adapter supports sending error response in exception subprocess. The error response body is part of expression ***$\{in.body\}***.
> 
> -   OData API response code is captured in the ***camelhttpresponsecode*** header.
> 
> -   OData adapter doesn’t support incoming payload in JSON format. The adapter only supports payload in XML format.
> 
> -   OData adapter doesn't support the word ***link*** in your payload. The word is reserved for creating reference links.
> 
> -   The adapter enables you to use connection pool while connecting to OData backend. For more information, see SAP Note [2863657](https://launchpad.support.sap.com/#/notes/2863657).
> 
> -   You can enable tracing for the adapter and analyze its log. For more information, see SAP Note [2852998](https://launchpad.support.sap.com/#/notes/2852998).

Select the *General* tab and provide values in the fields as follows.

<a name="loioc5c2e38e0c87472e996dfda04920bfc4__table_qpy_zcs_yjb"/>General


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

*Name*



</td>
<td valign="top">

Enter the name of the channel.



</td>
</tr>
</table>

Select the *Connection* tab and provide values in the fields as follows.

<a name="loioc5c2e38e0c87472e996dfda04920bfc4__table_g1y_2kw_wdb"/>Connection


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

URL of the OData V2 service that you want to connect to.



</td>
</tr>
<tr>
<td valign="top">

 *Proxy Type* 



</td>
<td valign="top">

The type of proxy you want to use for establishing connection with OData V2 service.

Currently, you can choose between *Internet* \(default\) and *On-Premise*.



</td>
</tr>
<tr>
<td valign="top">

*Location ID*

\(only if you choose *Proxy Type* as *On-Premise*\).



</td>
<td valign="top">

Location ID that you’ve configured in the cloud connector installed on your system.



</td>
</tr>
<tr>
<td valign="top">

 *Authentication* 



</td>
<td valign="top">

Authentication method that you want to use for connecting to the OData V2 service. Currently, you can choose from

-   *None*

-   *Basic*

-   *Principal Propagation*

    > ### Remember:  
    > When you want to use Principal Propagation as the authentication method to connect with an on-premise system, don't pass any authorization headers. Follow the approach recommended by SAP BTP Connectivity. See: [Authentication to the On-Premise System](https://help.sap.com/docs/CP_CONNECTIVITY/cca91383641e40ffbe03bdc78f00f681/67b0b94f09f2446598787eea0855e56b.html).


The following options are enabled only if you choose *Proxy Type* as *Internet*

-   *Client Certificate*

-   *OAuth2 Client Credentials*: Use this grant type to access web resources by authorizing the client application to perform required actions on behalf of a user.

-   *OAuth2 SAML Bearer Assertion*: If you've chosen this option, the identity of the user associated with the sender application is forwarded from the sender account to the receiver account.




</td>
</tr>
<tr>
<td valign="top">

*Credential Name*

\(only if you choose *Authentication* as *Basic*, *OAuth2 Client Credentials*, or *OAuth2 SAML Bearer Assertion*\).



</td>
<td valign="top">

Credential name of the credentials that you’ve deployed in *Security Material* section of :eye:.



</td>
</tr>
<tr>
<td valign="top">

*Private Key Alias*

\(only if you select *Client Certificate Authentication*\).



</td>
<td valign="top">

Enter the private key alias that enables the system to fetch the private key from keystore for authentication.

> ### Restriction:  
> The values ***true*** and ***false*** aren’t supported for this field.



</td>
</tr>
<tr>
<td valign="top">

 *CSRF Protected* 



</td>
<td valign="top">

Keep this option selected \(default setting\). It ensures that your integration flow is protected against Cross-Site-Request-Forgery, a kind of attack where a malicious party can perform harmful actions by masquerading as the logged in user



</td>
</tr>
</table>

Select the *Processing* tab and provide values in the fields as follows.

<a name="loioc5c2e38e0c87472e996dfda04920bfc4__table_tkx_3mw_wdb"/>Processing


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

 *Operation Details* 



</td>
<td valign="top">

The operation that you want to perform on the selected OData entity or resource. Supported operations are:

-   Query \(GET\)

-   Create \(POST\)

-   Update \(PUT\)

-   Merge

-   Read \(GET\)

-   Delete

-   Patch

-   Function Import


To leverage all operations, always use the latest version of the adapter.

> ### Note:  
> For non-GET operations, if the server responds with HTTP 2xx series code, the same response code is accepted for message processing.

For the *POST* operation, the automatic Primary Key generation is handled in 2 different ways based on the implementation in the backend server:

-   If the backend supports the primary key entry in the payload and later overwrites the entry value after receiving, you can enter a dummy value for the primary key.

-   If the primary key entry in the payload isn’t supported by the backend, then the payload must be sent without a primary key value. If mapping step is used, you can disable the entry by performing one of the following steps:
    -   Disable the primary key value in the mapping

    -   Manually remove the primary key entry from the schema and use that schema in mapping




</td>
</tr>
<tr>
<td valign="top">

 *Resource Path* 



</td>
<td valign="top">

Choose *Select* to launch the *Model Operation* wizard. Refer to table **Model Operation** for fields and description for model operation wizard.

> ### Note:  
> -   You can also specify the Resource Path parameter dynamically using a header or a property \(with an expression such like `${header.resourcePath}`, for example\). Note that, however, XPath expressions aren’t supported for this parameter.
> -   Navigation entities in the resource path aren’t supported.

> ### Note:  
> When you use this adapter with the Update or Merge operation, use the following format when specifying the value of the Resource Path parameter: `EntitySetName(key=value)` or`EntitySetName(key)`.
> 
> Example \(for EntitySetName=Product\):
> 
> `Product(productId='001')`



</td>
</tr>
<tr>
<td valign="top">

*Query Options*

\(enabled for *Query \(GET\)* and *Read \(GET\)* operations.\)



</td>
<td valign="top">

Query options that you’re passing as a part of the URI to the OData V2 service.



</td>
</tr>
<tr>
<td valign="top">

*Fields*

\(enabled for *Create \(POST\)*, *Merge \(MERGE\)*, *Patch \(PATCH\)*, and *Update \(PUT\)* operations.\)



</td>
<td valign="top">

Fields in the entity that you’re performing the operation on. If you use the Model Operation wizard, the input for this field is provided by the wizard.



</td>
</tr>
<tr>
<td valign="top">

 *Enable Batch Processing* 



</td>
<td valign="top">

Select to perform multiple operations in one request to the OData V2 service in the **$batch** mode.



</td>
</tr>
<tr>
<td valign="top">

 *Custom Query Options* 



</td>
<td valign="top">

Additional query options that aren’t available in the *Model Operation* wizard.



</td>
</tr>
<tr>
<td valign="top">

 *Content Type* 



</td>
<td valign="top">

Type of content that you’re sending to the OData V2 backend service. The adapter supports following content types:

-   *Atom* \(default\): Select this option to convert an XML payload to ATOM XML format.

-   *JSON*: Select this option to convert XML payload to JSON format.




</td>
</tr>
<tr>
<td valign="top">

*Content Type Encoding*

\(enabled for *Create \(POST\)*, *Merge \(MERGE\)*, *Patch \(PATCH\)*, and *Update \(PUT\)*, and *Function Import* operations.\)



</td>
<td valign="top">

Encoding type used for sending content to OData API.



</td>
</tr>
<tr>
<td valign="top">

 *Page Size* 



</td>
<td valign="top">

Maximum number of records that must be fetched in one page of results.

The value is set to *Empty* by default.

If no value is set, then Server-side pagination\(**\_\_next** link\) is considered.

If a value is entered, Client-side pagination is considered with the value provided.

> ### Note:  
> It’s recommended to leave the value *Empty*.



</td>
</tr>
<tr>
<td valign="top">

*Process in Page*

\(only when you’re performing the *Query \(GET\)* operation.\)



</td>
<td valign="top">

By selecting *Process in Pages*, you enable the adapter to process messages in batches. The size of a message is defined by the value that you specify for the *Page Size*.

To use *Process in Pages*, you must use the adapter in a *Local Integration Process* that is invoked by a *Looping Process Call* step. In the *Looping Process Call*, provide the loop condition details that follow:

-   Select *Expression Type* as *Non-XML*

-   For *Condition Expression*, provide ***$\{property.<receiver.name\>.<channel.name\>.hasMoreRecords\} contains 'true'***

-   For *Maximum Number of Iterations*, provide ***999***


This option isn’t enabled for *Content Enricher*.

> ### Note:  
> You can pass custom HTTP headers to OData receiver if you’ve defined the header in content modifier or script element and the element is placed before OData receiver adapter in an integration flow.



</td>
</tr>
<tr>
<td valign="top">

 *Timeout \(in min\)* 



</td>
<td valign="top">

Maximum time the adapter must wait for receiving a response from the OData V2 service.



</td>
</tr>
<tr>
<td valign="top">

 *HEADER DETAILS* 



</td>
<td valign="top">

*Request Headers*: Provide the **| \(Pipe\)**separated value list of HTTP request headers that has to be sent to the OData backend

If the value \* is entered, **all** the message headers are converted to HTTP request headers and forwarded.

*Response Headers*: Provide the **| \(Pipe\)** separated value list of HTTP response headers. The received header values will then be converted to message/exchange headers.

If the value \* is entered, **all** the HTTP response header values are converted to message/exchange headers.



</td>
</tr>
<tr>
<td valign="top">

 *Metadata Details* 



</td>
<td valign="top">

OData receiver adapter makes a $metadata call, before the actual endpoint call. Not all headers or query parameters are passed to the $metadata call. If your service needs some headers \(for example header ***apikey***, which is a customer authorization header to invoke API endpoints\) or parameters then you can provide the same in the request headers and query parameters.

Request headers provide comma-separated HTTP request headers to be sent to $metadata call. Custom query parameters enter key value pairs of query parameters, separated by *&* for multiple entries.

> ### Note:  
> The adapter stores the metadata cache for 1 hour after which it gets invalidated. The adapter looks out for the metadata again that can cause dips in performance every hour. If you face such dips every hour, you can use the message property ***SAP\_ODataV2\_RefreshCacheOnExpiry*** and set the value to ***false***. This can be done using a Content Modifier or Script step before the adapter. Upon using this property, the adapter stops invalidating the cache and looking for metadata every hour.



</td>
</tr>
</table>



## Modeling Operation

This adapter provides a wizard for modeling operations easily. It’s recommended that you use this wizard to ensure that the operation doesn’t contain any errors. The wizard can also fetch the *Externalized* parameters that are maintained under the *Connection* details of the OData receiver adapter.

There are two main steps in this wizard:

1.  *Connect to System:* In this step, you provide the details required for connecting to the Web Service that you’re accessing.
2.  *Select Entity and Define Operation:* In this step, you select the operation you want to perform and the entity on which you want to perform the operation on. After selecting the entity, you also select the fields, filtering and sorting conditions.
3.  *Configure Filter & Sorting:* This step is available only for data fetch operations, where you can define the order in which the records are fetched in the response payload and filter for the fields that you require.

<a name="loioc5c2e38e0c87472e996dfda04920bfc4__table_wqk_vjl_xdb"/>Connect to System


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

 *Connection Source* 



</td>
<td valign="top">

You can choose between *Remote* and *EDMX*.

If you choose *Remote*, you’ve to manually specify all the details like address and authentication details.

If you choose *Local EDMX File*, you select the service definition EDMX file that contains all these details that you specified manually when you selected *Remote*.



</td>
</tr>
<tr>
<td valign="top">

*Local EDMX File*

\(only if you select *Connection Source* as *Local EDMX File*\).



</td>
<td valign="top">

Choose *Select* to select the EDMX service schema. You can also manually upload it from your local file system.



</td>
</tr>
<tr>
<td valign="top">

 *Address* 



</td>
<td valign="top">

URL of the service that you want to access. If you’re connecting to an on-premise system, enter the *Virtual Host* in your Cloud Connector installation.



</td>
</tr>
<tr>
<td valign="top">

*Proxy Type*

\(only if you select *Connection Source* as *Remote*.\)



</td>
<td valign="top">

Type of proxy that you want to use to connect to the service.



</td>
</tr>
<tr>
<td valign="top">

*Location ID*

\(only if you select *Proxy Type* as *On-Premise*\).



</td>
<td valign="top">

Location ID that you’ve configured in the Cloud Connector installation.



</td>
</tr>
<tr>
<td valign="top">

 *Authentication* 



</td>
<td valign="top">

Only *Basic* authentication is supported. You can deploy credentials in :eye: and provide the *Credential Name* or provide the *Username* and *Password*.

For other authentication types, download the EDMX from the service and use the *Local EDMX File* to model the operation.



</td>
</tr>
</table>

<a name="loioc5c2e38e0c87472e996dfda04920bfc4__table_h45_knl_xdb"/>Select Entity & Define Operation


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

 *Operation* 



</td>
<td valign="top">

Select the operation that you want to perform.

The adapter supports *Function Import* for the following return types:

-   Entity

-   Collection of entities

-   Complex types

-   Collection of complex types

-   Simple types

-   Collection of simple types

-   Void


 *Function Import*can also be consumed in the *$batch* mode.



</td>
</tr>
<tr>
<td valign="top">

 *Sub-Levels* 



</td>
<td valign="top">

Sublevels of the entity that you want to access. For example, if you want to access the field *Description* in the entity *Products*, and the field is located at *Category* \> *Products* \> *Description*, you select the *Sub Levels* as ***3*** since the field you want to access is at the third level.



</td>
</tr>
<tr>
<td valign="top">

 *Select Entity* 



</td>
<td valign="top">

Entity that you want to perform the operation on.



</td>
</tr>
<tr>
<td valign="top">

 *Generate XML Schema Definition* 



</td>
<td valign="top">

Enable the check box if you want to generate an XSD file for the operation. You can also provide a name of your choice for the XSD file. This XSD file is needed when you create a message mapping.

There could be a scenario in which you wish to edit or update your modeling. In such cases, you can overwrite the XSD file instead of generating a new file every time.



</td>
</tr>
<tr>
<td valign="top">

 *Fields* 



</td>
<td valign="top">

Fields associated with the entity that you want to perform the operation on.



</td>
</tr>
<tr>
<td valign="top">

 *Top* 



</td>
<td valign="top">

Specifies the top 'n' number of entries to be fetched.

For more information, see **Top System Query Option \($top\)** in [OData V2 URI Conventions](http://www.odata.org/documentation/odata-version-2-0/uri-conventions/)



</td>
</tr>
<tr>
<td valign="top">

 *Skip* 



</td>
<td valign="top">

Specifies the top 'n' number of entries to be skipped and the rest of the entries are fetched.

For more information, see **Skip System Query Option \($skip\)** in [OData V2 URI Conventions](http://www.odata.org/documentation/odata-version-2-0/uri-conventions/).



</td>
</tr>
</table>

This step is available only for data fetch operations, *Query\(GET\), and* *Read\(GET\)*.

<a name="loioc5c2e38e0c87472e996dfda04920bfc4__table_gbn_y3m_xdb"/>Configure Filter & Sorting


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

 *Filter By* 



</td>
<td valign="top">

Select the field that you want to use as reference for filtering, choose the operation \(ex: *Less Than or Equal*\), and provide a value.

> ### Note:  
> The *IN* operation is available with filtering when editing the query manually. This operation isn’t available in the Query Modeling wizard.
> 
> The IN operator must be used in lower case in the query.
> 
> > ### Example:  
> > https://<hostname\>/odata/v2/User?$filter=userId in 'ctse1','mhuang1','flynch1'
> 
> For more information, see [Customized Operators](https://help.sap.com/docs/SAP_SUCCESSFACTORS_PLATFORM/d599f15995d348a1b45ba5603e2aba9b/ded5808b5edb4bc9a8acfb5e9fe1b025.html?version=latest).



</td>
</tr>
<tr>
<td valign="top">

 *Sort By* 



</td>
<td valign="top">

Select the field that you want to use as sorting parameter and choose *Ascending* or *Descending* order.



</td>
</tr>
</table>

