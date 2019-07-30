---
ms.topic: include
---

Configure the server that runs Azure DevOps Server to use an existing SMTP server for email alerts.

```
TfsConfig configureMail /Enabled:<true|false> /FromEmailAddress:<emailAddress> /SmtpHost:<SMTPHostName>
```

|Option|Description|
|---|---|
|FromEmailAddress|Specifies the address from which to send email notifications from Azure DevOps Server for a check in, work item assigned to you, or other notifications. This address is also checked for validity and, depending on your server configuration, might have to represent a valid email account on the mail server. If the address does not exist or is not valid, the default email address is used.|
|SmtpHost|Specifies the name of the server that hosts the mail server.|

### Prerequisites

To use the **configureMail** command, you must be a member of the Team Foundation Administrators security group on the Azure DevOps application-tier server. For more information, see [Permission reference for Azure DevOps Server](/azure/devops/security/permissions)

### Remarks

You can also [use the administration console](/azure/devops/server/admin/setup-customize-alerts) to configure Azure DevOps Server to use an SMTP server.

### Example

The following example shows the syntax used to configure the from email address to `TFS@contoso.com` and the SMTP mail server as `ContosoMailServer`:

```
TfsConfig configureMail /FromEmailAddress:TFS@contoso.com /SmtpHost:ContosoMailServer
```
