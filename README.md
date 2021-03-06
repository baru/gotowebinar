# GoToWebinar PHP wrapper

[![Latest Version](https://img.shields.io/github/release/paravibe/gotowebinar.svg?style=flat-square)](https://github.com/paravibe/gotowebinar/releases)
[![Build Status](https://img.shields.io/travis/paravibe/gotowebinar.svg?style=flat-square)](https://travis-ci.org/paravibe/gotowebinar)
[![Total Downloads](https://img.shields.io/packagist/dt/paravibe/gotowebinar.svg?style=flat-square)](https://packagist.org/packages/paravibe/gotowebinar)

## Installation
`composer require paravibe/gotowebinar`

## How to use

### Initialize client
`$client = new \LogMeIn\GoToWebinar\Client($access_token, $values);`

Where `$access_token` is a token retrived during authorization procedure - https://goto-developer.logmeininc.com/how-get-access-token-and-organizer-key  
and `$values` are response data that contain:
* account_key
* account_type
* email
* firstName
* lastName
* organizer_key

Use any method described here https://goto-developer.logmeininc.com/content/gotowebinar-api-reference-v2
by passing proper HTTP method and endpoint to `createRequest()` method.

### GET/DELETE methods
```php
$get = $client->createRequest('GET', "organizers/{$organizer_key}/webinars")->execute();
$data = $get->getDecodedBody();
```
### POST/PUT methods
```php
$post_data = array(
  'subject' => 'TEST',
  'description' => 'Test API integration',
  'times' => array(
    array(
      'startTime' => '2018-05-12T15:00:00Z',
      'endTime' => '2018-05-12T16:00:00Z',
    )
  ),
  'timeZone' => 'Europe/Kiev',
);

$new = $client->createRequest('POST', "organizers/{$organizer_key}/webinars")
  ->attachBody($post_data)
  ->execute();
```
