# Email

* [The All-New Guide to CSS Support in Email - Sep 2017](https://www.campaignmonitor.com/blog/email-marketing/2017/09/all-new-guide-css-support-email/)
* [Email Bugs Database](https://github.com/hteumeuleu/email-bugs)
* [Gmail finally support embedded `<style>`, `display: none` and media queries in Sept 2016](https://developers.google.com/gmail/design/css)
* [Email Client Market Share](https://emailclientmarketshare.com/)
* [Bojler is an email boilerplate and a guideline for writing HTML code](https://slicejack.github.io/bojler/getting-started)
* [Visual Email Builder Apps](https://css-tricks.com/visual-email-builder-apps/)

```html
<!-- If you want to disable auto-scaling -->
<meta name="x-apple-disable-message-reformatting">
```

Now that Gmail supports the style block in the `<head>`, inlining is no longer necessary when optimizing for Gmail.

* [Here's why Litmus didn't inline CSS for its first newsletter of 2017](https://litmus.com/community/discussions/6116-here-s-why-litmus-didn-t-inline-css-for-its-first-newsletter-of-2017)

## Samples

* [MailChimp Email Blueprints](https://github.com/mailchimp/email-blueprints)

## BCC

* [BCC Pitfalls: Why BCC Has No Place in your Email Marketing Strategy](https://www.sparkpost.com/blog/thou-shalt-not-bcc-pitfalls/)

## Media Queries

Because most email client do not have media queries support, we can't use mobile-first approach with `min-width`, rather we need to use `max-width` and go desktop-first.

```css
@media screen and (max-width: 600px) {
  .responsive-table {
    display: block;    width: 100% !important;
  }  .responsive-image {
    height: auto;
    max-width 100% !important;
  }
}
```

## DKIM - DomainKeys Identified Mail

* [PostMark DKIM Guide](https://postmarkapp.com/guides/dkim)
* An email security standard (http://www.dkim.org/)
* Why? It's easy to impersonate a trusted sender over SMTP
* Allow sender like (PostMark or AWS SES) to sign email on your behalf
* `DKIM-Signature` SMTP header
* This ensure message is authentic with regards to the domain
* Is optional, but it enhance deliverability with DKIM-compliant ISPs
* DKIM signatures are stored in your domain's DNS system
* Email address or domain has to be verified
* Only need to setup for "From" address, not for "Return-Path" or "Reply-To" address
* Not a universally adopted standard
* ISP use DKIM to build reputation on your domain over time
* Domains can have multiple public DKIM keys, and the selector value makes sure recipient servers use the correct one (e.g. `s=20170101pm; d=jobline.com.sg`)

## SPF - Sender Policy Framework

* Care about "Return-Path" only
* Can prevent abuse when combined with DKIM and DMARC
* Designed to combat email spoofing by specifying which mail servers are authorized to send email for their domain
* [SPF syntax](http://www.openspf.org/SPF_Record_Syntax)
* Don't ever use `-all` (it create more issues than it solves), use `~all`

In the past, email providers used From/Sender (or MAIL FROM??) to check for alignment. But now they using Return-Path instead.

**This is how we add both PostMark (not really required) and AWS SES:**

```
v=spf1 a mx include:spf.mtasv.net include:amazonses.com ~all
```

Try DIG command: `dig txt spf.mtasv.net`

## DMARC - Domain-based Message Authentication, Reporting and Conformance

* [DMARC.org](https://dmarc.org/)
* Newer standard that care about "From" address
* You can use DKIM to achieve DMARC validation, but it is a best practice to use both DKIM and SPF for maximum deliverability