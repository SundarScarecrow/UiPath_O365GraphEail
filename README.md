<b>Prerequisites:</b>

O365 - Connection enabled in Azure with client configured for desired AD users and email.

Assets with O365 Client ID, Value, Tenant ID

Asset Name: O365_ApplicationId; Type = Credential

Asset Name: O365_Value; Type = Credential

Asset Name: O365_TenantId; Type = Credential

<b>Input Arguments:</b>

Argument name: in_ToAddress; Type = String; Required

Argument name: in_CCAddress; Type = String; Optional

Argument name: in_BCCAddress; Type = String; Optional

Argument name: in_ToAddress; Type = IEnumerable<String>; Optional

Argument name: in_Body; Type = String; Required

Argument name: in_Subject; Type = String; Required

Argument name: in_Account; Type = String; Required

<b>Supported file types for Attachments:</b>

.xlsx, .xls, .zip, .jpg, .png, .txt, .csv, .pdf

New file types can be added in Switch with the correct FileContentType value


<b>How this works:</b>

With valid Asset values and input arguments, create a JSON object.

Append the values for Subject, Body, and Recipients.

For each attachment passed, convert the file into a Base64 Encoded string. Append the value of the encoded string and FileContentType into the JSON object.

Generate a bearer token for:<b> POST https://login.microsoftonline.com/{TenantID}/oauth2/token/</b>

Send email by requesting: <b>POST https://graph.microsoft.com/v1.0/users/{Email}/sendMail</b>

Payload the created JSON object
