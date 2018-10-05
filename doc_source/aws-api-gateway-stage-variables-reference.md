# Amazon API Gateway Stage Variables Reference<a name="aws-api-gateway-stage-variables-reference"></a>

 You can use API Gateway stage variables in the following cases\. 

## Parameter Mapping Expressions<a name="stage-variables-in-parameter-mapping-expressions"></a>

A stage variable can be used in a parameter mapping expression for an API method's request or response header parameter, without any partial substitution\. In the following example, the stage variable is referenced without the `$` and the enclosing `{...}`\. 
+ `stageVariables.<variable_name>`

## Mapping Templates<a name="stage-variables-in-mapping-templates"></a>

 A stage variable can be used anywhere in a mapping template, as shown in the following examples\. 
+  `{ "name" : "$stageVariables.<variable_name>"}`
+ `{ "name" : "${stageVariables.<variable_name>}"}`

## HTTP Integration URIs<a name="stage-variables-in-integration-HTTP-uris"></a>

A stage variable can be used as part of an HTTP integration URL, as shown in the following examples\.
+ A full URI without protocol, e\.g\., `http://${stageVariables.<variable_name>}`
+ A full domain: e\.g\., `http://${stageVariables.<variable_name>}/resource/operation`
+ A subdomain: e\.g\., `http://${stageVariables.<variable_name>}.example.com/resource/operation`
+ A path, e\.g\., `http://example.com/${stageVariables.<variable_name>}/bar`
+ A query string, e\.g\., `http://example.com/foo?q=${stageVariables.<variable_name>}` 

## AWS Integration URIs<a name="stage-variables-in-integration-aws-uris"></a>

 A stage variable can be used as part of AWS URI action or path components, as shown in the following example\.
+ `arn:aws:apigateway:<region>:<service>:${stageVariables.<variable_name>}`

## AWS Integration URIs \(Lambda Functions\)<a name="stage-variables-in-integration-lambda-functions"></a>

 A stage variable can be used in place of a Lambda function name, or version/alias, as shown in the following examples\. 
+ `arn:aws:apigateway:<region>:lambda:path/2015-03-31/functions/arn:aws:lambda::<account_id>:function:${stageVariables.<function_variable_name>}/invocations`
+ `arn:aws:apigateway:<region>:lambda:path/2015-03-31/functions/arn:aws:lambda::<account_id>:function:<function_name>:${stageVariables.<version_variable_name>}/invocations`

## AWS Integration Credentials<a name="stage-variables-in-integration-aws-credentials"></a>

 A stage variable can be used as part of AWS user/role credential ARN, as shown in the following example\. 
+  `arn:aws:iam::<account_id>:${stageVariables.<variable_name>}` 