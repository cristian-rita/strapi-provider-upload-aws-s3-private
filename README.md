# strapi-provider-upload-aws-s3-private

## Description

This version of provider is identical with the offical one [here](https://github.com/strapi/strapi/blob/master/packages/strapi-provider-upload-aws-s3/), the only difference being that the ACL: 'public-read' config is removed. 
This is useful if you want to keep the bucket private. 

### Important

Strapi is fetching the images by doing a client side request. You need to allow these request, otherwise the images won't show up in Strapi.

## Configurations

Your configuration is passed down to the provider. (e.g: `new AWS.S3(config)`). You can see the complete list of options [here](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/S3.html#constructor-property)

See the [using a provider](https://strapi.io/documentation/developer-docs/latest/development/plugins/upload.html#using-a-provider) documentation for information on installing and using a provider. And see the [environment variables](https://strapi.io/documentation/developer-docs/latest/setup-deployment-guides/configurations.html#environment-variables) for setting and using environment variables in your configs.

**Example**

`./config/plugins.js`

```js
module.exports = ({ env }) => ({
  // ...
  upload: {
    provider: 'aws-s3-private',
    providerOptions: {
      accessKeyId: env('AWS_ACCESS_KEY_ID'),
      secretAccessKey: env('AWS_ACCESS_SECRET'),
      region: env('AWS_REGION'),
      params: {
        Bucket: env('AWS_BUCKET'),
      },
    },
  },
  // ...
});
```

### Important

This is also working with IAM roles. You just need to omit the accessKeyId and secretAccessKey and AWS SDK will automatically select the IAM credentials.

```js
module.exports = ({ env }) => ({
  // ...
  upload: {
    provider: 'aws-s3-private',
    providerOptions: {
      region: env('AWS_REGION'),
      params: {
        Bucket: env('AWS_BUCKET'),
      },
    },
  },
  // ...
});
```

## Links

- [Strapi website](https://strapi.io/)
- [Strapi community on Slack](https://slack.strapi.io)
- [Strapi news on Twitter](https://twitter.com/strapijs)