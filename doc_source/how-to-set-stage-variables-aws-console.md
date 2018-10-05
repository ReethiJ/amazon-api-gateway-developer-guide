# Set Stage Variables Using the Amazon API Gateway Console<a name="how-to-set-stage-variables-aws-console"></a>

 In this tutorial, you will learn how to set stage variables for two deployment stages of a sample API, using the Amazon API Gateway console\. Before you begin, make sure the following prerequisites are met: 
+ You must have an API available in API Gateway\. Follow the instructions in [Creating an API in Amazon API Gateway](how-to-create-api.md)\.
+ You must have deployed the API at least once\. Follow the instructions in [Deploying an API in Amazon API Gateway](how-to-deploy-api.md)\.
+ You must have created the first stage for a deployed API\. Follow the instructions in [Create a New Stage](stages.md#how-to-create-stage-console)\.

**To Declare Stage Variables Using the API Gateway Console**

1. Sign in to the API Gateway console at [https://console\.aws\.amazon\.com/apigateway](https://console.aws.amazon.com/apigateway)\.

1.  Create an API, create a `GET` method on the API's root resource, if you have not already done so\. Set the HTTP **Endpoint URL** value as "`http://${stageVariables.url}`", and then choose **Save**\.   
![\[Set an HTTP GET endpoint URL with a stage variable\]](http://docs.aws.amazon.com/apigateway/latest/developerguide/images/stageVariables-set-http-get-url.png)

1.  Choose **Deploy API**\. Choose **New Stage** and enter "`beta`" for **Stage name**\. Choose **Deploy**\.   
![\[Deploy to beta stage\]](http://docs.aws.amazon.com/apigateway/latest/developerguide/images/stageVariables-deploy-beta-stage.png)

1. In the **beta Stage Editor** panel; choose the **Stage Variables** tab; and then choose **Add Stage Variable**\. 

1.  Enter the "`url`" string in the **Name** field and the "`httpbin.org/get`" in the **Value** field\. Choose the checkmark icon to save the setting for the stage variable\. 

1.  Repeat the above step to add two more stage variables: `version` and `function`\. Set their values as "`v-beta`" and "`HelloWorld`", respectively\. 
**Note**  
 When setting a Lambda function as the value of a stage variable, use the function's local name, possibly including its alias or version specification, as in **HelloWorld**, **HelloWorld:1** or **HelloWorld:alpha**\. Do not use the function's ARN \(for example, **arn:aws:lambda:us\-east\-1:123456789012:function:HelloWorld**\)\. The API Gateway console assumes the stage variable value for a Lambda function as the unqualified function name and will expand the given stage variable into an ARN\. 

1.  From the **Stages** navigation pane, choose **Create**\. For **Stage name**, type **prod**\. Select a recent deployment from **Deployment** and then choose **Create**\.   
![\[Create a new prod stage for an existing deployment\]](http://docs.aws.amazon.com/apigateway/latest/developerguide/images/stageVariables-create-prod-stage.png)

1.  As with the **beta** stage, set the same three stage variables \(**url**, **version**, and **function**\) to different values \("`petstore-demo-endpoint.execute-api.com/petstore/pets`", "`v-prod`", and "`HelloEveryone`"\), respectively\. 