# API Gateway Pricing<a name="api-gateway-pricing"></a>

 For general API Gateway region\-specific pricing information, see [Amazon API Gateway Pricing](https://aws.amazon.com/api-gateway/pricing/)\. 

The following lists the exceptions of the general pricing scheme:
+ API caching in Amazon API Gateway is not eligible for the AWS Free Tier\.
+ Calling methods with the [authorization type](https://docs.aws.amazon.com/apigateway/api-reference/resource/method/#authorizationType) of `AWS_IAM`, `CUSTOM`, and `COGNITO_USER_POOLS` are not charged for authorization and authentication failures\.
+ Calling methods requiring API keys are not charged when API keys are missing or invalid\.
+ API Gateway\-throttled requests are not charged when the request rate or burst rate exceeds the preconfigured limits\.
+ Usage plan\-throttled requests are not charged when rate limits or quota exceed the preconfigured limits\.