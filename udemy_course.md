# Udemy Course Verification Schema

## Data Source Name

Udemy - A global platform providing online courses on various topics, ranging from programming to personal development.

## API Endpoint

`GET https://www.udemy.com/api-2.0/users/me/subscribed-courses-instructors`

```json
{
  "count": 1,
  "next": null,
  "previous": null,
  "results": [
    {
      "_class": "user",
      "id": 21681922,
      "title": "Brad Traversy"
    }
  ]
}
```

## Technical Breakdown

This schema is used to verify that user has bought a specific course on Udemy. The schema is divided into two APIs. The first API is used to veriy that user has a udemy account. And the second API is used to check if the user has brought that specfic course or not. The value here is the course id if someone want to check if the user has broguht the course x then they can replace the value with the course id of course x.

## Schema Code

```json
{
  "issuer": "Udemy",
  "desc": "A global platform providing online courses on various topics, ranging from programming to personal development",
  "website": "https://www.udemy.com/home/my-courses/learning/",
  "APIs": [
    {
      "host": "www.udemy.com",
      "intercept": {
        "url": "api-2.0/contexts/me/",
        "method": "GET",
        "query": [
          {
            "header": "true",
            "verify": true
          }
        ]
      },
      "nullifier": "header|user|id"
    },
    {
      "host": "www.udemy.com",
      "intercept": {
        "url": "api-2.0/users/me/subscribed-courses/",
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
        }
      ]
    }
  ],
  "HRCondition": ["verify you have bought the course"],
  "tips": {
    "message": "When you successfully log in and click on the course, please click the 'Start' button to initiate the verification process."
  }
}
```
