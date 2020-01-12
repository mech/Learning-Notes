# FileMaker

* [Soliant Consultant](https://www.soliantconsulting.com/filemaker)
* [Data Integration](https://www.filemaker.com/learning/custom-app-academy/205/overview.html)

## Uninstall FileMaker

* [Get Mojave from AppStore direct link](https://itunes.apple.com/us/app/macos-mojave/id1398502828?mt=12)

Sometimes we may have problem with FileMaker server installation especially when upgrading new macOS or new FileMaker server.

* [Reinstalling FileMaker Server to troubleshoot an issue](https://support.filemaker.com/s/article/Reinstalling-FileMaker-Server-to-troubleshoot-an-issue-1503693085688?language=en_US)

If you need to upgrade FileMaker server, you need to stop it first.

```
▶ sudo launchctl stop com.filemaker.fms
```

## FileMaker 17

* [System Requirements for FileMaker Server 17](https://support.filemaker.com/s/article/System-Requirements-for-FileMaker-Server-17?language=en_US)
* [System Requirements for FileMaker Server 18](https://support.filemaker.com/s/article/System-Requirements-for-FileMaker-Server-18?language=en_US)
* [Deprecated and removed features in FileMaker 17](https://support.filemaker.com/s/answerview?language=en_US&anum=000026028)
* [Edit Privilege Set](http://docs.360works.com/index.php/Enable_XML_FileMaker_17)

## Enable Custom Web Publishing

Must be enabled using CLI.

Starting from FileMaker 17, it is much harder to enable XML. We need to go into CLI to perform it. See [360Works document on Enable XML FileMaker 17](http://docs.360works.com/index.php/Enable_XML_FileMaker_17)

```
▶ fmsadmin set cwpconfig enablexml=true
▶ fmsadmin restart wpe -y
```

Visit: 

* http://localhost/fmi/xml/FMPXMLRESULT.xml?-dbnames
* http://localhost/fmi/xml/fmresultset.xml?-dbnames

## Apache Web Server

macOS comes with its own Apache Web Server. Most of the time, FM will use it also for CWP. Just in case you need to know where FileMaker's Apache configuration is located. A well-configured FileMaker should not have to do the following though.

```
▶ cd /Library/FileMaker\ Server/HTTPServer/bin/
▶ sudo ./httpdctl start/stop/restart
```

## SSL with Let's Encrypt

* [Let's Encrypt SSL Certificates for FileMaker Server for Mac](https://bluefeathergroup.com/blog/lets-encrypt-ssl-certificates-for-filemaker-server-for-mac/)
* [Request for using Let's Encrypt](https://community.filemaker.com/en/s/idea/0870H000000fyCcQAI/detail)

## Data API

* [2GB per month limit](https://community.filemaker.com/thread/186361)
* [FileMaker 17 Data API Costs for More Data - Good discussion on data limit](https://community.filemaker.com/en/s/question/0D50H00006dsjnzSAA/filemaker-17-data-api-costs-for-more-data)

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
* [Search Features](https://app.works/community/training-tutorials/search-features/)


