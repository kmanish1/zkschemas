# Spotify Plan Verification Schema

## Data Source Name

Spotify is a leading global audio streaming service that provides access to millions of songs, podcasts, and audio content.

## API Endpoint

`GET https://www.spotify.com/in-en/api/account/v1/datalayer/`

JSON Response

```json
{
  "isTrialUser": null,
  "currentPlan": "free",
  "isRecurring": null,
  "daysLeft": null,
  "accountAgeDays": 1556,
  "isSubAccount": null,
  "country": "IN",
  "nextBillingInfo": null,
  "expiry": null
}
```

## Technical Breakdown

This schema is used to verify if the user is on a free plan or a premium plan. The API endpoint returns the user's current plan. If the user is on a free plan, the `currentPlan` key will have the value `free`. If the user is on a premium plan, the `currentPlan` key will have a value other than `free`. The schema checks if the `currentPlan` key is not equal to `free` to verify that the user is on a premium plan.

## Schema Code

```json
{
  "issuer": "Spotify",
  "desc": "Spotify is a leading global audio streaming service that provides access to millions of songs, podcasts, and audio content.",
  "website": "https://www.spotify.com/in-en/account/overview",
  "APIs": [
    {
      "host": "www.spotify.com",
      "intercept": {
        "url": "in-en/api/account/v1/datalayer",
        "method": "GET"
      },
      "assert": [
        {
          "key": "currentPlan",
          "value": "free",
          "operation": "!="
        }
      ],
      "nullifier": "isTrialUser"
    }
  ],
  "HRCondition": ["Verify that you have bought spotify subscription"],
  "tips": {
    "message": "When you successfully log in, please click the 'Start' button to initiate the verification process."
  }
}
```
