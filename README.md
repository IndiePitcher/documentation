# IndiePitcher.com REST API Dodumentation
IndiePitcher is an all in one tool for your software company to send transactional, marketing, or cold emails.

## Transactional Emails
Transactional emails is a fancy name for sending emails such as "You've been invited to organization Another ChatGpt Wrapper Startup on IndiePitcher.com as an admin." or "Your invoice 123456 has been paid.". IndiePitcher provides an easy to use a company email you already have (integrated using STMP) to start sending highly customizable and personalized transactional emails. 

Here's what's currently supported:
- Send a raw plaintext / markdown / html email. Format personalized emails with the help of markdown syntax, or use full html templates.
- Predefine a template on IndiePitcher.com and send just personalization data
- Track email opens
- Track link clicks
- Add a tag to group your transactional emails
- Add unsubscribe button to sign out of emails for selected tag
- We make sure you don't send an email to an email that has unsubscribed so you don't have to

### Raw Transactional Email

```bash
curl -X POST https://api.indiepitcher.com/v1/email/send_raw
   -H 'Content-Type: application/json'
   -H "Authorization: Bearer {YOUR API TOKEN}"
   -d '{"subject":"Welcome to IndiePitcher","body":"Your email content", "bodyType": "plaintext", "recipientEmail": "john@example.com", "category": "onboarding"}'
```

| Property | Type | Is Required | Description
| --- | --- | --- | --- |
| subject | string | yes | The subject line of your email. |
| bodyType | string | yes | Notifies us if the email body is a plaintext string, a markdown string we'll parse, or a raw html we'll just enrich by link tracking if requested and pass along. Accepted values are `plaintext`, `markdown`, `html`. Read bellow how to include a link to unsubscribe. |
| recipientEmail | string | yes | The email of the recipient of this message |
| category | string | no | You can group transactional emails into categories. This is useful for when a user taps unsubscibe, you can limit his unsibscribe only to emails for a given category. It can only contain ASCII letters (a–z, A–Z), numbers (0–9), underscores (_), or dashes (-). |
| emailAccountId | string | no | You can integrate IndiePitcher with more than one email account. This property allows you to choose which account you want to send the email from. Ommiting this value will pick one of your integrated accounts. |
| rejectIfUnsubscribedForCategory | bool | no | Rejects to send the email if given user previously unsibscribed from receiving email for given category. Defaults to `true`. |
| rejectIfUnsubscribedAnywhere | bool | no | Rejects to send the email if given user previously unsibscribed to any of your emails sent through IndiePitcher. Defaults to `false`. |
| trackOpens | bool | no | Choose if you wish to track when the recipient opens your email (when available). Default value is `true`. This has no effect if if `bodyType` is set to `plaintext`. |
| trackLinkOpens | bool | no | Choose if you wish to track when the recipient opens links in your email. This will proxy the links through our servers. Default value is `false`. This has no effect if if `bodyType` is set to `plaintext`. |

---

### Transactional Email from Template

```bash
curl -X POST https://api.indiepitcher.com/v1/email/send_from_template
   -H 'Content-Type: application/json'
   -H "Authorization: Bearer {YOUR API TOKEN}"
   -d '{"templateId":"154ad6fa-3f22-49be-8e56-c8e3bfb02373","variables": {"firstName": "John"}, "recipientEmail": "john@example.com", "category": "onboarding"}'
```

| Property | Type | Is Required | Description
| --- | --- | --- | --- |
| templateId | string | yes | The id of a template crated in the IndiePitcher dashboard. |
| variables | string: string dictionary | no | Provide an array of variables to personalize the template with, such as the first name of the recipient. |
| recipientEmail | string | yes | The email of the recipient of this message |
| category | string | no | You can group transactional emails into categories. This is useful for when a user taps unsubscibe, you can limit his unsibscribe only to emails for a given category. It can only contain ASCII letters (a–z, A–Z), numbers (0–9), underscores (_), or dashes (-). |
| emailAccountId | string | no | You can integrate IndiePitcher with more than one email account. This property allows you to choose which account you want to send the email from. Ommiting this value will pick one of your integrated accounts. |
| rejectIfUnsubscribedForCategory | bool | no | Rejects to send the email if given user previously unsibscribed from receiving email for given category. Defaults to `true`. |
| rejectIfUnsubscribedAnywhere | bool | no | Rejects to send the email if given user previously unsibscribed to any of your emails sent through IndiePitcher. Defaults to `false`. |
| trackOpens | bool | no | Choose if you wish to track when the recipient opens your email (when available). Default value is `true`. This has no effect if if `bodyType` is set to `plaintext`. |
| trackLinkOpens | bool | no | Choose if you wish to track when the recipient opens links in your email. This will proxy the links through our servers. Default value is `false`. This has no effect if if `bodyType` is set to `plaintext`. |

---

That's it for now, but there's a lot more to come, such as support for webhooks. Don't hesitate to reach out to petr@indiepitcher.com for any feedback, suggestions, bugs.

