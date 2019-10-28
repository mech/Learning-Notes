# Introduction

* [Rails Development Dependencies Install](http://guides.rubyonrails.org/development_dependencies_install.html)
* [Efficient Rails DevOps - A book](https://efficientrailsdevops.com/)
* [Tools for a Modern Ruby Development Setup](https://www.sitepoint.com/tools-for-a-modern-ruby-development-setup/)
* [Modular Monolith Rails](https://medium.com/@dan_manges/the-modular-monolith-rails-architecture-fb1023826fc4)
* [Prevention of god classes and OOP](https://medium.com/root-engineering/separating-data-and-code-in-rails-architecture-3a031e17706b)

```ruby
# Look for config/payments.yml
Rails.application.config_for(:payments)['stripe_key']

# Use configuration file for globals
if registered_at < Rails.application.config_for(:registration)['limit'].minutes.ago
end
```

> The boundary between stateful and stateless logic helps us think about implementing some of our most complex business logic in pure Ruby, completely separated from Rails. This is the key point to modular Rails application.

## Architecture and File Structure

* [Rails Parts](http://tomrothe.de/posts/rails_parts.html)

## Upgrade

* [Official guide on upgrading Rails](http://edgeguides.rubyonrails.org/upgrading_ruby_on_rails.html)

### 6

* [What's coming to Rails 6.0?](https://medium.com/rubyinside/whats-coming-to-rails-6-0-8ec79eea66da)
* [Zeitwerk integration](https://github.com/rails/rails/pull/35235)
* [Goodbye Sprockets. Welcome Webpacker](https://medium.com/@coorasse/goodbye-sprockets-welcome-webpacker-3-0-ff877fb8fa79)

### 5.1

* [Ruby on Rails 5.1.0 Deprecations](https://blog.driftingruby.com/ruby-on-rails-5-1-0-deprecations/)

### 4

* [What's new in Active Record - Rails 4 Countdown to 2013](http://blog.remarkablelabs.com/2012/12/what-s-new-in-active-record-rails-4-countdown-to-2013)

## ActionCable

* [anycable](https://github.com/anycable/anycable)
* [Realtime with React and Rails](https://blog.codeship.com/realtime-with-react-and-rails/)
* [Using Rails 5 ActionCable and RethinkDB to build a Reactive WebSocket App](https://medium.com/rubyinside/using-rails-5-actioncable-and-rethinkdb-to-build-a-reactive-websocket-app-7f77382cfb5)
* [Action Cable 'Hello World' with Rails 5.1](https://medium.com/rubyinside/action-cable-hello-world-with-rails-5-1-efc475b0208b)

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

* [Shopify gem for making jobs interruptible and resumable](https://github.com/Shopify/job-iteration)
* [sidekiq-scheduler](https://github.com/moove-it/sidekiq-scheduler)
* [rufus-scheduler](https://github.com/jmettraux/rufus-scheduler)
* [Pub/Sub for Sidekiq](https://github.com/hired/reactor)
* [**wisper-activejob**](https://github.com/krisleech/wisper-activejob)
* [Beyond Validates_Presence_of: Ensuring Eventual Consistency](https://www.youtube.com/watch?v=QpbQpwXhrSI)
* [Real World Rails Background Jobs](https://www.eliotsykes.com/real-world-rails-background-jobs)
* [Evented Rails: Decoupling complex domains in Rails with Domain Events](https://blog.carbonfive.com/2017/07/18/evented-rails-decoupling-complex-domains-in-rails-with-domain-events/)

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
* **Always send email with deliver_later, even if it is inside background job already**

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

```ruby
class SendDailyTriageEmailJob < ApplicationJob
  def perform(user)
    return false if before_email_time_of_day?(user)
    return false if email_sent_in_last_24_hours?(user)
    return false if skip_daily_email?(user)
    
    send_daily_triage!(user)
  end
end
```

## Bad Press

* [My time with Rails is up](http://solnic.eu/2016/05/22/my-time-with-rails-is-up.html)

## Rails 5

* [What's new in Rails 5](http://blog.michelada.io/whats-new-in-rails-5)

## Blog

* [Bogdan](https://bogdanvlviv.com/posts.html)
* [Using Dotenv In Rails](http://metaskills.net/2013/10/03/using-dotenv-in-rails/)
* [AkitaOnRails](http://www.akitaonrails.com/?locale=en)
* [solnic.eu](http://solnic.eu/)
* [Michael Cordell - Reading Ruby Code](https://blog.mikecordell.com/)
* [Nathan Long](http://nathanmlong.com/blog/)

## Example Applications

* [Application for Applying To (an) Employment Tribunal](https://github.com/ministryofjustice/atet/issues)
* [homeland](https://github.com/ruby-china/homeland)

## Videos

* [Perusing the Rails Source Code](https://www.youtube.com/watch?v=Q_MpGRfnY5s)
* [Ruby Australia](https://www.youtube.com/channel/UCr38SHAvOKMDyX3-8lhvJHA/videos)

