# Epic Games Account Verification Schema

## Data Source Name

Epic Games is a popular video game company that has been around for over 30 years. They are known for their popular games such as FIFA, Madden NFL, and The Sims. Epic Games has a large user base and is a popular choice for gamers of all ages.

## API Endpoint

`GET https://www.epicgames.com/account/v2/api/email/info`

Sample JSON Reponse:

```json
{
  "isSuccess": true,
  "data": {
    "canUpdateEmail": true,
    "canUpdateNext": "",
    "default": {
      "email": "t***u@gmail.com",
      "verified": true,
      "default": true
    },
    "lastEmailUpdate": null,
    "unverified": null
  }
}
```

## Technical Breakdown

This schema is to verify that user has a verfied epic games account. We check this by intercepting the email info api in which we check if the email is verified or not. If the email is verified, we nullify the email in the response.

## Schema Code

```json
{
  "issuer": "Epic Games",
  "desc": "EA Games is a popular video game company that has been around for over 30 years. They are known for their popular games such as FIFA, Madden NFL, and The Sims. EA Games has a large user base and is a popular choice for gamers of all ages.",
  "website": "https://www.epicgames.com/account/personal",
  "APIs": [
    {
      "host": "www.epicgames.com",
      "intercept": {
        "url": "account/v2/api/email/info",
        "method": "GET"
      },
      "assert": [
        {
          "key": "data|default|verfied",
          "value": "true",
          "operation": "="
        }
      ],
      "nullifer": "data|default|email"
    }
  ],
  "HRCondition": ["Verify that your have EA games account"],
  "tips": {
    "message": "When you successfully log in, please click the 'Start' button to initiate the verification process."
  }
}
```
