EzUrlScannerBundle
==================

An eZPublish/eZPlatform bundle designed to assist in url-scanning the current website.

## Usecases

The main scenario that it aims to support is the following: after a site has been developed, make sure that there are no urls available to the public which have been left _unintentionally_ unprotected, and allow access to private or confidential data.

## Features

This bundle should do 2 things:

1. produce a list of urls from all known eZ-legacy and Symfony routes, to be used with any penetration testing tool of choice
    - using a minimal set of rules for creating permutations on route parameters
    - also, well known eZ-specific non-php routes should be included, such as f.e. /var/storage/..., /settings/... or /extension/xxx/settings/...

2. provide a simple penetration testing tool to scan all of the URLs in the above list, taking into account eZ-specific requirements, such as f.e.:
    - logged-in scan & logged-out scan
    - scan the whole list of urls multiple times, with different hostnames (siteaccess testing)
    - scan the whole list of urls twice, once with http and once with https (check for proper redirection to https)
    - scan each url first as logged-in user then as anon user (check for unintended cache sharing by Varnish)
    
    And the ususal minimum set of features for a web scanner:
    - report number of responses per type: 200, 30x, 40x, 50x
    - variable wait time between requests
    - variable number of concurrent requests
    - allow custom http headers
    - allow basic auth instead of session auth

## Non-features

- parsing html and retrieveing all of the urls from browsing the site (use existing tools from that)

- parsing webserver access logs and retrieveing all of the urls from them (are there good tools for this?)

## Why not using an existing pen testing tool instead?

I have had over time the questionable pleasure of going through multiple penetration-testing reports carried out on websites published by the eZPublish/eZPlatform CMS.
Although they have often provided real value, feeding to the developer team unexpected findings, they have also, more often than not, produced a considerable amount of false positives and low-value discoveries, while at the same time missing out some glaring configuration problems.
This is not necessarily the fault of an incompetent pen tester or low quality tool: it is in general one of the downsides of black-box testing. It is also compounded by the highly dynamic nature of websites powered by CMS platforms.

In any case, the common, best-case outcome of the pen-testing exercise seems to be:
- developers fix all the reported, low-risk issues
- the pen testers run the scan again, and see all green
- everybody on the project feels good. PO pats PM on the back, PM pays dev team a round of beers
- no one wants to waste any more time on security issues
- any manually-driven pen test (aka. white-box test) is either cancelled or procastinated ad infinity

What this tool aims to achieve is to increase the value of automated testing by providing the pen testers with the knowledge that normally is only available to seasoned eZ developers, in a form that can be quickly digested and acted upon.
