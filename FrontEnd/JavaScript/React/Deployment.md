# Deployment

* [How to deploy a live ReactJS to AWS](https://hackernoon.com/how-to-deploy-a-live-reactjs-redux-website-in-under-10-minutes-cadf73cfc75a)
* [Deploying create-react-app to S3 and CloudFront](https://medium.com/@omgwtfmarc/deploying-create-react-app-to-s3-or-cloudfront-48dae4ce0af)
* [Serverless Stack](http://serverless-stack.com/)
* [How To Build a React GraphQL Static Site Served From AWS CloudFront](https://cosmicjs.com/blog/how-to-build-a-react-graphql-static-site-served-from-aws-cloudfront)

```
location / {
  if (!-e $request_filename) {
    rewrite ^(.*)$ /index.html break;
  }
}
```

