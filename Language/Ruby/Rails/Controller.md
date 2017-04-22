# Rails Controller

* [How DHH Organizes His Rails Controllers](http://jeromedalbert.com/how-dhh-organizes-his-rails-controllers/)
* [Examining The Internals Of The Rails Request/Response Cycle](http://www.rubypigeon.com/posts/examining-internals-of-rails-request-response-cycle/)
* [How to Reduce Controller Bloat with Interactors in Ruby](https://semaphoreci.com/community/tutorials/how-to-reduce-controller-bloat-with-interactors-in-ruby)

## Routes

```ruby
resources :sessions, only: [:create, :show]

resources :users do
  post :activate, on: :collection
  resources :followers
end
```

## Serializers

```ruby
has_many :followers, serializer: Api::V1::UserSerializer
```