EzUrlScannerBundle
==================

An eZPublish/eZPlatform bundle designed to assist in url-scanning the current website.

## Usecases

The main scenario that it aims to support is the following: after a site has been developed, are we sure that there are no urls available to the public which have been left _unintentionally_ unprotected, and allow access to private data?

## Features

This bundle should do 2 things:

1. produce a list of urls from all known eZ-legacy and Symfony routes, to be used with any penetration testing tool of choice
  - also, well known eZ-specific non-php routes should be included, such as f.e. /var/storage/..., /settings/... or /extension/xxx/settings/...
  - using a minimal set of rules for creating permutations on route parameters

2. provide a simple penetration testing tool to scan all of the URLs in the above list, taking into account eZ-specific requirements, such as f.e.:
    - logged-in scan vs. logged-out scan
    - scan the whole list of urls multiple times, with different hostnames
 And the ususal minimum set of features for a web scanner:
    - variable wait time between requests
    - variable number of concurrent requests
    - allow custom http headers
    - allow basic auth instead of session auth

## Non-features

- parsing html and retrieveing all of the urls from browsing the site (use existing tools from that)

- parsing webserver access logs and retrieveing all of the urls from them (are there good tools for this?)

