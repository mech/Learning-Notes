# Amazon SES

Allow you to send bulk or transactional emails from your application.

* [How EmailOctopus built an email marketing platform using Amazon SES](https://aws.amazon.com/blogs/ses/guest-post-how-emailoctopus-built-an-email-marketing-platform-using-amazon-ses/)

```ruby
config.action_mailer.delivery_method = :smtp
config.action_mailer.smtp_settings = {
  address: 'email-smtp.us-west-2.amazonaws.com',
  port: '25', # 465 or 587 
  user_name: ENV["AWS_SES_USERNAME"],
  password: ENV["AWS_SES_PASSWORD"],
  authentication: :login,
  enable_starttls_auto: true
}
```

Note: The SMTP username and password is not the same as the AWS access key ID and secret access key, so don't mix it up.

## Limits

* [Limits in Amazon SES](https://docs.aws.amazon.com/ses/latest/DeveloperGuide/limits.html)

## Bounces and Complaints

Hard bounce has 2 types:

1. **Permanent** - you should never send to that recipient again.
2. **Transient** - ISP is not accepting messages but you can try again later after some time. For example message too large or content error.

If you don't handle complaints from ISPs, it will affect your deliverability.