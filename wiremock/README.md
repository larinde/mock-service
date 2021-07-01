# Mocking with Wiremock

## Starting Wiremock

``` bash
 java -jar wiremock-standalone-2.26.1.jar  --port 5000 
```

http://localhost:8080/mock-service/mapping/__admin/

## Recording with Wiremock

``` bash
java -jar wiremock-standalone-2.14.0.jar --port 9000 --proxyall http://localhost/accounting/v1/invoices
```



1. create a folder for recording

``` bash
 mkdir insight-app-recording
 cd  insight-app-recording
 
```
2. start service to be recorded

``` bash
 ./gradlew build 
 ./gradlew bootRun 
```
 
3. run wiremock as a recording proxy service in the recording folder
 
``` bash
 java -jar ../wiremock-jre8-standalone-2.29.0.jar --port 9000 --proxy-all http://localhost:8080/graphql --record-mappings

```

4. Invoke the service via the proxy uri

```
http://localhost:9000

```

5. End the recording and view the recording in the created recording folder
  - **__files** contain the response message payload
  - **mappings** contain the mapping of request to response messages, including a description of the



6. To playback the recording start wiremock from the recording folder and hit the proxy endpoint with the same requests as in the recording

``` bash
 java -jar ../wiremock-jre8-standalone-2.29.0.jar --port 9000

```

## Stubbing via REST API

To stubbs to wire mock:
 - define the message pair
 - expected HTTP behaviour
 - post the stubb to the __admin/mappings endpoint
 
The stubb below simulates an HTTP OK response with a 5 second delay 


```
curl --verbose -X POST \
--data '{
      "request": {
        "method": "GET",
        "url": "/mock/api/portfolios"
      },
      "response": {
        "status": 200,
        "fixedDelayMilliseconds": 1000,
        "headers": {
          "Content-Type": "application/json"
        },
        "jsonBody": {
          "size": 3,
          "currency": "EUR",
          "portfolios": [
            {
              "portfolioName": "Interactive Investor - ISA",
              "accountType": "ISA",
              "totalValue": 1234.77,
              "lastUpdated": "2020-06-28T16:53:20.000Z"
            },
            {
              "portfolioName": "Interactive Investor - Trading",
              "accountType": "Trading",
              "totalValue": 300.31,
              "lastUpdated": "2020-06-28T16:53:20.000Z"
            },
            {
              "portfolioName": "ING - Trading",
              "accountType": "Trading",
              "totalValue": 386.05,
              "lastUpdated": "2020-06-28T16:53:20.000Z"
            }
          ]
        }
      }
}'  \
'http://localhost:9000/__admin/mappings' 

```
 
## Resetting Wiremock mappings in a browser

http://localhost:9000/__admin/mappings/


## Resetting Wiremock mappings in a browser

http://localhost:9000/__admin/mappings/mappings/reset

