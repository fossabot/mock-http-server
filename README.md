# mock-http-server
[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2Fcsdavide%2Fmock-http-server.svg?type=shield)](https://app.fossa.com/projects/git%2Bgithub.com%2Fcsdavide%2Fmock-http-server?ref=badge_shield)

A minimal java mock server for soap/rest test
## Getting Started
### Build
```
mvn clean package => target\mockserver-1.0.0-jar-with-dependencies.jar
```
### Usage
```
java -jar mockserver.jar <port> <path_response>
```  
* port : listening port's server
* path_response = path of replies
### Example
#### SOAP
##### Prepare
> Request.xml ( Body = testResources )
```xml
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" 
                  xmlns:ns="http://my.request.namespace/">
 <soapenv:Body>
  <ns:testResources />
 </soapenv:Body>
</soapenv:Envelope>
```
> <path_response>/testResources.xml
```xml
<ns:testResourcesResponse xmlns:ns="http://my.response.namespace/">
 <return>true</return>
</ns:testResourcesResponse>
```
##### Execute
> java -jar mockserver.jar 9080 <path_response>

> curl --data "@Request.xml" http://localhost:9080/service/soap
```xml
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
 <soap:Body>
  <ns:testResourcesResponse xmlns:ns="http://my.response.namespace/">
   <return>true</return>
  </ns:testResourcesResponse>
 </soap:Body>
</soap:Envelope>
```
#### REST
##### Prepare
> <path_response>/testResources.json
```json
{
  "testResourcesResponse": {
    "return": "true"
  }
}
```
##### Execute
> java -jar mockserver.jar 9080 <path_response>

> curl http://localhost:9080/service/rest?method=testResources
```json
{
  "testResourcesResponse": {
    "return": "true"
  }
}
```


## License
[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2Fcsdavide%2Fmock-http-server.svg?type=large)](https://app.fossa.com/projects/git%2Bgithub.com%2Fcsdavide%2Fmock-http-server?ref=badge_large)