# Behat SEO Contexts

[![Latest Version](https://img.shields.io/github/release/mortola/behat-seo-contexts.svg?style=flat-square)](https://github.com/mortola/behat-seo-contexts/releases)
[![Build Status](https://img.shields.io/travis/mortola/behat-seo-contexts.svg?style=flat-square)](https://travis-ci.org/mortola/behat-seo-contexts)
[![Quality Score](https://img.shields.io/scrutinizer/g/mortola/behat-seo-contexts.svg?style=flat-square)](https://scrutinizer-ci.com/g/mortola/behat-seo-contexts)
[![Total Downloads](https://img.shields.io/packagist/dt/mortola/behat-seo-contexts.svg?style=flat-square)](https://packagist.org/packages/mortola/behat-seo-contexts)

**Behat extension for testing some On-Page SEO factors.**

Includes contexts for testing:
* title / meta description
* canonical
* hreflang
* meta robots
* robots.txt
* indexation: tests meta robots + robots.txt + X-Robots-Tag header
* redirects
* sitemap validation (inc. multilanguage)
* HTML validation
* assets performance 
* more...

Installation
------------

Basic requirements:

* PHP 7.1+
* Behat 3+
* Mink + Mink extension

### How to install it

1. [Install Composer](https://getcomposer.org/download/)
2. Execute:

```
$ composer require mortola/behat-seo-contexts --dev
```

3. Add the Context you need to `behat.yml`:

```yaml
# behat.yml
default:
    # ...
    suites:
        default:
          contexts:
            - MOrtola\BehatSEOContexts\Context\MetaContext
            - MOrtola\BehatSEOContexts\Context\LocalizationContext
            - MOrtola\BehatSEOContexts\Context\RobotsContext
            - MOrtola\BehatSEOContexts\Context\IndexationContext
            - MOrtola\BehatSEOContexts\Context\RedirectContext
            - MOrtola\BehatSEOContexts\Context\SitemapContext
            - MOrtola\BehatSEOContexts\Context\HTMLContext
            - MOrtola\BehatSEOContexts\Context\PerformanceContext
            - MOrtola\BehatSEOContexts\Context\SocialContext

```
### Featured steps
##### MetaContext
```gherkin
Then the page canonical should not be empty
Then the page canonical should be :expectedCanonicalUrl
Then the page title should not be empty
Then the page title should be :expectedTitle
Then the page meta description should not be empty
Then the page meta description should be :expectedMetaDescription
Then the page meta robots should be noindex
Then the page meta robots should not be noindex
```
##### LocalizationContext
```gherkin
Then the page hreflang markup should be valid
```
##### RobotsContext
```gherkin
Given I am a :crawlerUserAgent crawler
Then I should not be able to crawl :resource
Then I should be able to crawl :resource
Then I should be able to get the sitemap URL
```
##### IndexationContext
```gherkin
Then the page should be indexable
Then the page should not be indexable
```
##### RedirectContext
```gherkin
Given I follow redirects
Given I do not follow redirects
Then I should be redirected to :url
```
##### SitemapContext
```gherkin
Given the sitemap :sitemapUrl
Then the sitemap should be valid
Then the index sitemap should be valid
Then the multilanguage sitemap should be valid
Then the index sitemap should have a child with URL :childSitemapUrl
Then /^the sitemap should have ([0-9]+) children$/
Then the multilanguage sitemap should pass Google validation
Then the sitemap URLs should be alive
Then /^(\d+) random sitemap URLs? should be alive$/
```
##### HTMLContext
```gherkin
Then the page HTML markup should be valid
Then /^the page HTML5 doctype declaration should (not |)be valid$
```
##### PerformanceContext
```gherkin
Then /^browser cache should be enabled for (.+\..+|external|internal) (png|jpeg|gif|ico|js|css) resources$/
Then /^Javascript code should load (async|defer)$/
Then HTML code should be minified
Then CSS code should be minified
Then Javascript code should be minified
Then CSS code should load deferred
Then critical CSS code should exist in head
```
##### SocialContext
```gherkin
Then /^the (Twitter|Facebook) Open Graph data should satisfy (minimum|full) requirements$/
```

### Examples
This library is self-tested, and you can find examples inside the [features directory](./tests/features).
Feel free to explore it to discover each step definition.

Useful tips
------------
* Use [Symfony KernelDriver](https://github.com/Behat/Symfony2Extension) for improving the performance if you are working in a Symfony project.
