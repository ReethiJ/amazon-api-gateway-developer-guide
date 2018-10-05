# x\-amazon\-apigateway\-integration Object<a name="api-gateway-swagger-extensions-integration"></a>

 Specifies details of the backend integration used for this method\. This extension is an extended property of the [Swagger Operation](https://github.com/swagger-api/swagger-spec/blob/master/versions/2.0.md#operationObject) object\. The result is an [API Gateway integration](https://docs.aws.amazon.com/apigateway/api-reference/resource/integration/) object\. 


**Properties**  

| Property Name | Type | Description | 
| --- | --- | --- | 
| cacheKeyParameters | An array of string | A list of request parameters whose values are to be cached\. | 
| cacheNamespace | string | An API\-specific tag group of related cached parameters\. | 
| connectionId | string | The ID of a [VpcLink](https://docs.aws.amazon.com/apigateway/api-reference/resource/vpc-link/) for the private integration\. | 
| connectionType | string | The integration connection type\. The valid value is "VPC\_LINK" for private integration or "INTERNET", otherwise\. | 
| credentials | string |  For AWS IAM role\-based credentials, specify the ARN of an appropriate IAM role\. If unspecified, credentials will default to resource\-based permissions that must be added manually to allow the API to access the resource\. For more information, see [Granting Permissions Using a Resource Policy](https://docs.aws.amazon.com/lambda/latest/dg/intro-permission-model.html#intro-permission-model-access-policy)\. Note: when using IAM credentials, please ensure that [AWS STS regional endpoints](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_temp_enable-regions.html) are enabled for the region where this API is deployed for best performance\.   | 
| contentHandling | string | Request payload encoding conversion types\. Valid values are 1\) CONVERT\_TO\_TEXT, for converting a binary payload into a Base64\-encoded string or converting a text payload into a utf\-8\-encoded string or passing through the text payload natively without modification, and 2\) CONVERT\_TO\_BINARY, for converting a text payload into Base64\-decoded blob or passing through a binary payload natively without modification\. | 
| httpMethod | string |  The HTTP method used in the integration request\. For Lambda function invocations, the value must be POST\.  | 
| passthroughBehavior | string |  Specifies how a request payload of unmapped content type is passed through the integration request without modification\. Supported values are when\_no\_templates, when\_no\_match, and never\. For more information, see [Integration\.passthroughBehavior](https://docs.aws.amazon.com/apigateway/api-reference/resource/integration/#passthroughBehavior)\. | 
| requestParameters | [x\-amazon\-apigateway\-integration\.requestParameters Object](api-gateway-swagger-extensions-integration-requestParameters.md) | Specifies mappings from method request parameters to integration request parameters\. Supported request parameters are querystring, path, header, and body\. | 
| requestTemplates | [x\-amazon\-apigateway\-integration\.requestTemplates Object](api-gateway-swagger-extensions-integration-requestTemplates.md) | Mapping templates for a request payload of specified MIME types\. | 
| responses | [x\-amazon\-apigateway\-integration\.responses Object](api-gateway-swagger-extensions-integration-responses.md) | Defines the method's responses and specifies desired parameter mappings or payload mappings from integration responses to method responses\.  | 
| timeoutInMillis | integer | Integration timeouts between 50 ms and 29,000 ms\. | 
| type | string |  The type of integration with the specified backend\. The valid value is  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/apigateway/latest/developerguide/api-gateway-swagger-extensions-integration.html) For more information about the integration types, see [integration:type](https://docs.aws.amazon.com/apigateway/api-reference/resource/integration/#type)\.  | 
| uri | string | The endpoint URI of the backend\. For integrations of the aws type, this is an ARN value\. For the HTTP integration, this is the URL of the HTTP endpoint including the https or http scheme\. | 

## x\-amazon\-apigateway\-integration Example<a name="api-gateway-swagger-extensions-integration-example"></a>

 The following example integrates an API's `POST` method with a Lambda function in the backend\. For demonstration purposes, the sample mapping templates shown in `requestTemplates` and `responseTemplates` of the examples below are assumed to apply to the following JSON\-formatted payload: `{ "name":"value_1", "key":"value_2", "redirect": {"url" :"..."} }` to generate a JSON output of `{ "stage":"value_1", "user-id":"value_2" }` or an XML output of `<stage>value_1</stage>`\. 

```
"x-amazon-apigateway-integration" : {
    "type" : "aws",
    "uri" : "arn:aws:apigateway:us-east-1:lambda:path/2015-03-31/functions/arn:aws:lambda:us-east-1:012345678901:function:HelloWorld/invocations",
    "httpMethod" : "POST",
    "credentials" : "arn:aws:iam::012345678901:role/apigateway-invoke-lambda-exec-role",
    "requestTemplates" : {
                "application/json" : "#set ($root=$input.path('$')) { \"stage\": \"$root.name\", \"user-id\": \"$root.key\" }",
                "application/xml" : "#set ($root=$input.path('$')) <stage>$root.name</stage> "
    },
    "requestParameters" : {
        "integration.request.path.stage" : "method.request.querystring.version",
        "integration.request.querystring.provider" : "method.request.querystring.vendor"
    },
    "cacheNamespace" : "cache namespace",
    "cacheKeyParameters" : [],
    "responses" : {
        "2\\d{2}" : {
            "statusCode" : "200",
            "responseParameters" : {
                "method.response.header.requestId" : "integration.response.header.cid"
            },
            "responseTemplates" : {
                "application/json" : "#set ($root=$input.path('$')) { \"stage\": \"$root.name\", \"user-id\": \"$root.key\" }",
                "application/xml" : "#set ($root=$input.path('$')) <stage>$root.name</stage> "
            }
        },
        "302" : {
            "statusCode" : "302",
            "responseParameters" : {
                "method.response.header.Location" : "integration.response.body.redirect.url"
            }
        },
        "default" : {
            "statusCode" : "400",
            "responseParameters" : {
                "method.response.header.test-method-response-header" : "'static value'"
            }
        }
    }
}
```

Note that double quotes \("\) of the JSON string in the mapping templates must be string\-escaped \(\\"\)\. 