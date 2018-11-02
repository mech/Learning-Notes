# FileMaker

* [Soliant Consultant](https://www.soliantconsulting.com/filemaker)
* [Data Integration](https://www.filemaker.com/learning/custom-app-academy/205/overview.html)

## Data API

* [2GB per month limit](https://community.filemaker.com/thread/186361)

## Query

Be careful with `=` and `==` when doing FM query.

```ruby
# Will match:
# SRID="S6414-old"
# SRID="S6414 old"
Renewal::RenewalOption.where(service_code: '=S6414').total
```

Anytime there is a dash or space, using single equal is not enough to match total string. Use double equal to be safer.

```ruby
# Will NOT match:
# SRID="S6414-old"
# SRID="S6414 old"
Renewal::RenewalOption.where(service_code: '==S6414').total
```

## Relationship Graph

* [A Little Relationship Advice and Anchor Buoy](https://medium.com/filemaker/a-little-filemaker-relationship-advice-and-anchor-buoy-84e1be88e3a0)

## People

* [Martha Zink](https://twitter.com/mz123)

## Videos

* [Soliant TV](https://www.youtube.com/user/SoliantConsultingTV/videos)
* [Integration session videos](https://www.youtube.com/playlist?list=PLkvKnBkQSCeSvp0mzwQAuqSTSeJOaZv35)


