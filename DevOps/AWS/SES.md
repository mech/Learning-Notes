# Amazon SES

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

## Limits

* [Limits in Amazon SES](https://docs.aws.amazon.com/ses/latest/DeveloperGuide/limits.html)