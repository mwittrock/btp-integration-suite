<!-- loio72c8fa737dde41ddb0403018174f57f8 -->

# Deploying an OAuth2 Client Authorization Code with Generic Provider

Create an OAuth2 Client Authorization Code with the Generic Provider.



<a name="loio72c8fa737dde41ddb0403018174f57f8__context_axq_4s2_kmb"/>

## Context

Cloud Integration supports OAuth Clients with various update processes for their refresh tokens:

-   *Refresh Tokens that expire and are invalidated*: There are some OAuth clients that create a new refresh token that automatically and immediately invalidates the old refresh token. This means, the old refresh token can no longer be used as soon the new refresh token is available.

    Example: OAuth Client of GoToWebinar;

-   *Refresh Tokens that don't expire*: There are OAuth clients whose refresh token don't expire. In this case the refresh token doesn’t need to be updated at all.


> ### Note:  
> The following update processes aren't supported:
> 
> -   OAuth Clients with refresh tokens that do expire but that can't be updated \(rotated\) aren't supported, since the connection doesn't work anymore after the refresh token has expired. This applies, for instance, to the SAP XSUAA OAuth client.
> 
> -   OAuth Clients which require proprietary parameters for updating the refresh token in the token request, for instance Microsoft 365, which will only return the refresh token in the token request, if you specify the scope "offline\_access". See: [Deploying an OAuth2 Client Authorization Code with Microsoft 365 as Provider](deploying-an-oauth2-client-authorization-code-with-microsoft-365-as-provider-04a94b1.md).

There are OAuth clients which require additional query parameters in the token or authorization URL.

SAP Integration Suite supports these kinds of OAuth clients. You can just specify these parameters in the URL, for example:

-   the *Google OAuth client* requires the additional query parameters "prompt=consent" and "access\_type=offline" in the authorization URL: https://accounts.google.com/o/oauth2/v2/auth?prompt=consent&access\_type=offline;

-   the *Dropbox client* requires the additional query parameter "token\_access\_type=offline" in the authorization URL: https://www.dropbox.com/oauth2/authorize?client\_id=<app\_id\>&token\_access\_type=offline&response\_type=code&redirect\_uri=http%3A%2F%2Flocalhost%2Fcode&state=123;


> ### Caution:  
> -   The update of the Refresh Token must occur at least 2 days before the Refresh Token expires.
> 
> -   A refresh token must not be invalidated by a succeeding refresh token before 20 per cent of the expiry period is reached.
> 
> -   The Access Token expiry period must be at least 30 min. We recommend an expiry period of 1 hour.
> 
> -   The maximum number of OAuth2 Authorization Code credentials is 500 \(including the Microsoft 365 credentials\).
> 
> -   You can't use the same OAuth Client that supports only one valid Refresh Token in one point in time in more than one OAuth2 Authorization Code credential with the same user.



<a name="loio72c8fa737dde41ddb0403018174f57f8__steps_cnq_ss2_kmb"/>

## Procedure

1.  Click the tile in the *Manage Security Material* section.

2.  Choose *Create* \> *OAuth2 Authorization Code*.

3.  Specify the following attributes:

    <a name="loio72c8fa737dde41ddb0403018174f57f8__table_mmz_35s_2y"/>


    <table>
    <tr>
    <th valign="top">

    Attribute


    
    </th>
    <th valign="top">

    Description


    
    </th>
    </tr>
    <tr>
    <td valign="top">

    Name


    
    </td>
    <td valign="top">

    Name of the artifact that you want to deploy on the tenant.


    
    </td>
    </tr>
    <tr>
    <td valign="top">

    Description


    
    </td>
    <td valign="top">

    Description of the artifact you're deploying on the tenant.


    
    </td>
    </tr>
    <tr>
    <td valign="top">

    Provider


    
    </td>
    <td valign="top">

    Enter the name of the provider of the platform on which you created the OAuth2 client.


    
    </td>
    </tr>
    <tr>
    <td valign="top">

    Authorization URL


    
    </td>
    <td valign="top">

    Provide the Authorization URL for authorizing the OAuth client to access resources of a user.

    You can add also additional query parameters, as described at the beginning of this chapter. Be aware that the following query parameters are added automatically: `client_id=<client_id>&response_type=code&redirect_uri=<url encoded redirect uri>&state=<state guid>&scope=<scope>`. The scope query part is only added if the scope attribute is not empty, see below.


    
    </td>
    </tr>
    <tr>
    <td valign="top">

    Token Service URL


    
    </td>
    <td valign="top">

    Provide the URL that generates the OAuth2 access and refresh token for the registered OAuth2 client and the provided user.

    You can add also additional query parameters, as described at the beginning of this chapter. The scope attribute \(see below\) is added as query parameter automatically in case of the "authorization\_code" grant type request; the scope attribute is not added in case of the "refresh\_token" grant type request.


    
    </td>
    </tr>
    <tr>
    <td valign="top">

    Client ID


    
    </td>
    <td valign="top">

    ID of the client you want to connect to.


    
    </td>
    </tr>
    <tr>
    <td valign="top">

    Client Secret


    
    </td>
    <td valign="top">

    Secret key of the client that you're connecting to.

    See: [OAuth 2.0](../40-RemoteSystems/oauth-2-0-3823134.md#loio382313443b8d4453b0fd536b82b9e15d).


    
    </td>
    </tr>
    <tr>
    <td valign="top">

    Send As


    
    </td>
    <td valign="top">

    -   Body Parameter: Send the Client ID and Client Secret in the request body when calling the Authorization URL or Token Service URL.

    -   Basic Auth Header: Send the Client ID and Client Secret via Basic Authorization when calling the Authorization URL or Token Service URL.



    
    </td>
    </tr>
    <tr>
    <td valign="top">

    User Name


    
    </td>
    <td valign="top">

    Name of the user whose resources the OAuth2 client gets access to.


    
    </td>
    </tr>
    <tr>
    <td valign="top">

    Scope


    
    </td>
    <td valign="top">

    OAuth2 scopes protecting the access to the resources.

    The scope value is added to the Authorization URL \(see above\) as query parameter and is also added to the Token Service URL, in case of the "authorization\_code" grant type request; but is not added to the Token Service URL in case of the "refresh\_token" grant type request \(see above\).

    > ### Note:  
    > If you add more than 1 scope, you need to separate your scopes by a blank space.


    
    </td>
    </tr>
    </table>
    
    > ### Note:  
    > Test your new setup regularly in the beginning, to waterproof the functionality of your setup. Especially test the replacement of refresh tokens, whether they expire or the new refresh token invalidates the old refresh token.

4.  Choose *Deploy*.


**Related Information**  


[Managing Security Material](managing-security-material-b8ccb53.md "The Manage Security Material area provides an overview of security-related artifacts.")

[OAuth 2.0](../40-RemoteSystems/oauth-2-0-3823134.md#loio382313443b8d4453b0fd536b82b9e15d "OAuth 2.0 allows a user to grant a client access to a protected resource (hosted by a resource server). The user typically restricts the access of the client and doesn't allow full access.")

[Deploying an OAuth2 Client Authorization Code with Microsoft 365 as Provider](deploying-an-oauth2-client-authorization-code-with-microsoft-365-as-provider-04a94b1.md "")

