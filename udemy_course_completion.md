# Verification Schema

## Data Source Name

Udemy - A global platform providing online courses on various topics, ranging from programming to personal development.

## API Endpoint

`GET https://www.udemy.com/api-2.0/users/me/subscribed-courses/?queryparams.....`
sample JSON response -

```json
{
  "results": [
    {
      "_class": "course",
      "id": 1646980
      "completion_ratio": 8,
      },
    }
  ]
}
```

## Technical Breakdown
Verifies that the user has successfully completed a course on Udemy, often required for certifications or employment validation.


## Schema Code

```json
{
  "issuer": "Udemy",
  "desc": "A global platform providing online courses on various topics, ranging from programming to personal development.",
  "website": "https://www.udemy.com/home/my-courses/learning/",
  "APIs": [
    {
      "host": "www.udemy.com",
      "intercept": {
        "url": "api-2.0/users/me/subscribed-courses",
        "method": "GET",
        "query": [
          {
            "ordering": "-last_accessed",
            "verify": false
          },
          {
            "fields[course]": "archive_time,buyable_object_type,completion_ratio,enrollment_time,favorite_time,features,image_240x135,image_480x270,is_practice_test_course,is_private,is_published,last_accessed_time,num_collections,published_title,title,tracking_id,url,visible_instructors",
            "verify": false
          },
          {
            "fields[user]": "@min,job_title",
            "verify": false
          },
          {
            "page": "1",
            "verify": false
          },
          {
            "page_size": "12",
            "verify": false
          },
          {
            "is_archived": "false",
            "verify": false
          }
        ]
      },
      "assert": [
        {
          "key": "results|?=0|id",
          "value": "1646980",
          "operation": "="
        },
        {
          "key": "results|?=0|completion_ratio",
          "value": "100",
          "operation": "="
        }
      ],
      "nullifier": "results|0|id"
    }
  ],
  "HRCondition": [
    "verify you have bought the course and successfully completed it 100%"
  ],
  "tips": {
    "message": "When you successfully log in and click on the course, please click the 'Start' button to initiate the verification process."
  }
}
```
