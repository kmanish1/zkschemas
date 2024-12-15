# Monkeytype Speed Verification Schema

## Data Source Name

MonkeyType is one of the popular platforms for typing practice to improve speed and accuracy. It offers a variety of typing tests and exercises to help users improve their typing skills. The platform also provides users with detailed statistics and analysis of their typing performance, including words per minute (WPM), accuracy, and more.

## API Endpoint

`GET https://api.monkeytype.com/users`
Sample JSON Response

```json
{
  "data": {
    "uid": "T24m4yl9V5OrECLkZeEm6p27z5T2",
    "personalBests": {
      "time": {
        "30": [
          {
            "acc": 94.92,
            "consistency": 70.4,
            "difficulty": "normal",
            "raw": 74.37,
            "wpm": 74.37,
            "timestamp": 1728981588160,
            "numbers": false
          }
        ]
      }
    }
  }
}
```

## Technical Breakdown

This schema verifys the typing speed of the user on the monkeytype platform. The schema checks if the user's typing speed is greater than 50 WPM. If the user's typing speed is greater than 50 WPM, the schema will consider the verification as successful. MonkeyType also provides the data for various other type of tests so devs can easily customize the schema to verify other type of tests as well.

Other type of data include like 15 seconds, 60 seconds, 120 seconds in the time domain and in the words domain 10 words and 100 words. In the schema we are verifying the wpm(words per minute). There are other data available like accuracy, consistency.

## Schema Code

```json
{
  "issuer": "MonkeyType",
  "desc": "A platform for typing practice to improve speed and accuracy.",
  "website": "https://monkeytype.com/account",
  "APIs": [
    {
      "host": "api.monkeytype.com",
      "intercept": {
        "url": "users",
        "method": "GET"
      },
      "assert": [
        {
          "key": "data|personalBests|time|30|0|wpm",
          "value": "50",
          "operation": ">"
        }
      ],
      "nullifier": "data|uid"
    }
  ],
  "HRCondition": ["Typing speed greater than 50 WPM"],
  "tips": {
    "message": "When you successfully log in, please click the 'Start' button to initiate the verification process."
  }
}
```
