# DoraHacks Account Verification Schema

## Data Source Name

Dorahacks is a global hacker movement and open-source developer community that supports hackathons, bounties, and grants to empower innovation in blockchain, AI, and emerging technologies.

## API Endpoint

Sample JSON Response:
`GET https://dorahacks.io/api/tophackers/profile/170249/`

```json
{
  "hacker_id": 170249,
  "uuid": "66f840146fcf392640915489feedb615",
  "username": "U_1fd0543db4173b",
  "nick_name": "thrishank"
}
```

## Technical Breakdown
This schema verifies the existence of a verified DoraHacks account using the DoraHacks API. The API response is intercepted at the api/tophackers/profile/ endpoint. The username field is checked to ensure it is not empty, confirming the account's validity. To maintain privacy, the uuid field is nullified in the response. The verification confirms only the account's existence without revealing sensitive details.

## Schema Code

```json
{
  "issuer": "DoraHacks",
  "desc": "Dorahacks is a global hacker community enabling innovation through hackathons, bounties, and grants.",
  "website": "https://dorahacks.io/home",
  "APIs": [
    {
      "host": "dorahacks.io",
      "intercept": {
        "url": "api/tophackers/profile/?=?",
        "method": "GET"
      },
      "assert": [
        {
          "key": "username",
          "value": " ",
          "operation": "!="
        }
      ],
      "nullifer": "uuid"
    }
  ],
  "HRCondition": ["Verify that you have a dorahacks Account"],
  "tips": {
    "message": "When you successfully log in, please click the 'Start' button to initiate the verification process."
  }
}
```
