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

## Resetting Wiremock mappings


http://localhost:9000/__admin/mappings/mappings/reset
http://localhost:9000/__admin/mappings/


