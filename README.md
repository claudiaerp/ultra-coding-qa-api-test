# ultra-coding-qa-api-test
ultra-coding-qa-api-test

## Purpose of the project:
The expected outcome is a Postman collection covering the testing of one of the 4 REST API resources.
For this project I have used https://dummy.restapiexample.com/ (since the other option did not work for me)

## Prerequisites:
To use this project you will need:
* Install [Postman](https://www.postman.com/downloads/) 
* Install [Node](http://nodejs.org)
* Install newman $ npm install -g newman

Notes: 
* Node and newman are optional, go for them in case you need to run the collection from your terminal.
* In case you decide to use newman, make sure you create a **reports** folder in the root of the project

## Setup:
* `git clone https://github.com/claudiaerp/ultra-coding-qa-api-test.git`
* Import environment and collection in Postman

## Using newman:
To run the collection using newman and generate a basic xml report, do:
```
newman run collection/ultra-api-test.postman_collection.json -e environment/ultra-api-test-environment.postman_environment.json --delay-request=60000 --reporters cli,junit --reporter-junit-export reports/result.xml
```

## Testing strategy explanation:
My first concern is functional testing, I need to ensure that the API functions properly.
The test cases fall into the following general test scenario groups:

* Basic positive tests (happy paths)
* Negative testing with invalid input

1. Basic positive tests (happy paths)
* Execute API call with valid required parameteres

| Test Action Category | Test Action Description  |
|:--------------------:| ------------------------:|
| Validate status code | Returned status code is – 200 OK |
| Validate headers | Verify that HTTP headers are as expected, content-type |
| Validate payload | Response is a well-formed JSON object |
| Validate payload information | Returned types are correct and data is reliable |

2. Basic negative tests
* Missing required parameters
* Attempting to pull a resource that does not exist (e.g., employee id not present in DB, invalid employee id (abc123), no id at all)
* Attempting to delete a resource that does not exist (e.g., employee id not present in DB, invalid employee id (abc123), no id at all)
* Attempting to update a resource that does not exist (e.g., employee id not present in DB, invalid employee id (abc123), no id at all)

| Test Action Category | Test Action Description |
|:--------------------:| ------------------------:|
| Validate status code | Returned status code is – 400 OK |
| Validate headers | Verify that HTTP headers are as expected, content-type |
| Validate payload | Response is a well-formed JSON object, error is received, it is clear and descriptive |