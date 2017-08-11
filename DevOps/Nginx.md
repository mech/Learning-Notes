# Nginx

* [Scriptability with Lua](https://openresty.org/en/)

```
http {
  client_max_body_size 10M;
}
```

## Monitoring

* [Nginx Amplify](https://amplify.nginx.com/signup/)

## HTTP/2

To solve latency issues, HTTP/2 uses multiplexing. This does not mean you don't do concatenation anymore. In fact you still need to do it. Just split it up intelligently.

* [HTTP/2 FAQ](https://http2.github.io/faq)
* [The Right Way to Bundle Your Assets for Faster Sites over HTTP/2](https://medium.com/@asyncmax/the-right-way-to-bundle-your-assets-for-faster-sites-over-http-2-437c37efe3ff#.2qypy2vsy)

## TCP Slow Start

* Linux Kernels > 2.6.39 enable IW10 by default. See [Make TCP faster](https://googlecode.blogspot.sg/2012/01/lets-make-tcp-faster.html)
* IW10 (14kb initial size)
* Stream large responses to the browser: `Transfer-Encoding: Chunked`
* [Reverse engineering Amazon and the Guardian - David Fox (LookZook)](https://www.safaribooksonline.com/library/view/fluent-conference-2017/9781491985298/video311523.html)
* [Designing Speed with Progressive Enhancement](https://www.youtube.com/watch?v=cdv8UQu96PU)


## BOTS

* [Bad Bots](http://www.botreports.com/badbots/index.shtml)

## SSL

PCI Security Council deprecated SSLv3 and TLS 1.0 for commercial transactions.

* [SSL and TLS Deployment Best Practices](https://github.com/ssllabs/research/wiki/SSL-and-TLS-Deployment-Best-Practices)
* [Is TLS fast yet?](https://istlsfastyet.com/)
* [SSL upgrades on rubygems.org and RubyInstaller versions](https://gist.github.com/luislavena/f064211759ee0f806c88)
* [The Guardian has moved to HTTPS](https://www.theguardian.com/info/developer-blog/2016/nov/29/the-guardian-has-moved-to-https)
* [Get HTTPS for free!](https://gethttpsforfree.com/)
* [SO: Are HTTPS URLs encrypted?](https://stackoverflow.com/questions/499591/are-https-urls-encrypted/499602#499602)
* [CertBot](https://certbot.eff.org/)
* [Video: Browser Security in 2017](https://www.youtube.com/watch?v=vvZRYUBFX-8)
* [Nginx Doc: Configuring HTTPS servers](https://nginx.org/en/docs/http/configuring_https_servers.html)

---

* BEAST attack - 2011
* Logjam attack - 2015
* As of Jan 2016, you can't get SHA1 cert anymore. Use SHA256.

### Checklist

* OCSP stapling enabled?
* HTTP Strict Transport Security (HSTS) policy declared?