# Introduction

* [Rails Development Dependencies Install](http://guides.rubyonrails.org/development_dependencies_install.html)
* [Efficient Rails DevOps - A book](https://efficientrailsdevops.com/)
* [Tools for a Modern Ruby Development Setup](https://www.sitepoint.com/tools-for-a-modern-ruby-development-setup/)

```ruby
# Look for config/payments.yml
Rails.application.config_for(:payments)['stripe_key']

# Use configuration file for globals
if registered_at < Rails.application.config_for(:registration)['limit'].minutes.ago
end
```

## ActionCable

* [Realtime with React and Rails](https://blog.codeship.com/realtime-with-react-and-rails/)

## Performance

* [**Rails Speed**](https://www.railsspeed.com/)
* [Speedshop Blog](https://www.speedshop.co/blog/)

## Deployment

* [Ruby in Production: Lessons Learned](https://medium.com/@rdsubhas/ruby-in-production-lessons-learned-36d7ab726d99)
* [Dockerize a Rails 5, Postgres, Redis, Sidekiq and Action Cable Application with Docker Compose](https://nickjanetakis.com/blog/dockerize-a-rails-5-postgres-redis-sidekiq-action-cable-app-with-docker-compose)
* [Your App Server Config is Wrong: Workers count and threads count](https://www.youtube.com/watch?v=itbExaPqNAE)
* [oink - Log parser to identify actions which significantly increase VM heap size](https://github.com/noahd1/oink)
* [Scaling Ruby apps to 1000RPM](https://www.speedshop.co/2015/07/29/scaling-ruby-apps-to-1000-rpm.html)
* [How To Scale Ruby on Rails Applications Across Multiple Droplets](https://www.digitalocean.com/community/tutorials/how-to-scale-ruby-on-rails-applications-across-multiple-droplets-part-1)
* [Video - Scaling Shopify to 300M uniques per month running Rails, Docker, MySQL with Simon Eskildsen](https://www.youtube.com/watch?v=yg3YnnFjw2Y)

```
passenger_max_request_time
worker_timeout
```

## Background Job

* [sidekiq-scheduler](https://github.com/moove-it/sidekiq-scheduler)
* [rufus-scheduler](https://github.com/jmettraux/rufus-scheduler)
* [Pub/Sub for Sidekiq](https://github.com/hired/reactor)
* [wisper-activejob](https://github.com/krisleech/wisper-activejob)
* [Beyond Validates_Presence_of: Ensuring Eventual Consistency](https://www.youtube.com/watch?v=QpbQpwXhrSI)
* [Real World Rails Background Jobs](https://www.eliotsykes.com/real-world-rails-background-jobs)

Network failures:

* Cannot connect
* Service partially completes work; never responds
* Service completes work; network cuts out at response
* Service completes work; sees client side timeout and rolls back
* Retry? Idempotency? Keep on trying?
* Creates or deletes?
* Circuit breakers?
* **We want eventual consistency!**
* Be kind to your downstream services (i.e. Slack notifier, Twitter, GeoTagging, etc.)
* Roll back, roll forward
* Timestamp your service to coalesce

```ruby
class SendAnalyticsEmailJob < ActiveJob::Base
  def perform
    Group.with_analytics.find_each do |group|
      BaseMailer.send_bulk_mail(to: group.admins) do |user|
        UserMailer.delay(priority: 10).analytics(user: user, group: group)
      end
    end
  end
end
```

## Bad Press

* [My time with Rails is up](http://solnic.eu/2016/05/22/my-time-with-rails-is-up.html)

## Rails 5

* [What's new in Rails 5](http://blog.michelada.io/whats-new-in-rails-5)

## Blog

* [Using Dotenv In Rails](http://metaskills.net/2013/10/03/using-dotenv-in-rails/)
* [AkitaOnRails](http://www.akitaonrails.com/?locale=en)
* [solnic.eu](http://solnic.eu/)
* [Michael Cordell - Reading Ruby Code](https://blog.mikecordell.com/)

## Example Applications

* [Application for Applying To (an) Employment Tribunal](https://github.com/ministryofjustice/atet/issues)
* [homeland](https://github.com/ruby-china/homeland)

## Videos

* [Perusing the Rails Source Code](https://www.youtube.com/watch?v=Q_MpGRfnY5s)
* [Ruby Australia](https://www.youtube.com/channel/UCr38SHAvOKMDyX3-8lhvJHA/videos)