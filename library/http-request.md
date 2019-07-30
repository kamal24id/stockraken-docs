---
description: >-
  StocKraken HTTP Request is a set of lightweight HTTP libraries available in
  multiple languages, built and maintained by clickoding. Base on Unirest for
  PHP.
---

# Stockraken HTTP Request \(Delay\)

## Features

* Utility methods to call `GET`, `HEAD`, `POST`, `PUT`, `DELETE`, `CONNECT`, `OPTIONS`, `TRACE`, `PATCH` requests
* Supports form parameters, file uploads and custom body entities
* Supports gzip
* Supports Basic, Digest, Negotiate, NTLM Authentication natively
* Customizable timeout
* Customizable default headers for every request \(DRY\)
* Automatic JSON parsing into a native object for JSON responses

## Requirements

* [cURL](http://php.net/manual/en/book.curl.php)
* PHP 5.4 or above
* [Unirest For PHP](http://unirest.io/php.html)
* Codeigniter 3.x \(this library work on CI\)

## Installation

### 1. [Codeigniter ](https://www.codeigniter.com/)3.X

StocKraken HTTP Request work for Codeigniter project, first you need install codeigniter 3.x.

For instruction installation codeigniter, [Read this article](https://www.codeigniter.com/user_guide/installation/index.html).

{% hint style="info" %}
 StocKraken HTTP Request is library for Codeigniter, that's why you should install in codeigntier project.
{% endhint %}

### 2. Unirest For PHP

#### Using [Composer](https://getcomposer.org/)

To install unirest-php with Composer, just add the following to your `composer.json` file:

```javascript
{
    "require-dev": {
        "mashape/unirest-php": "3.*"
    }
}
```

or by running the following command in your codeigniter folder project:

```bash
composer require mashape/unirest-php
```

on linux especial ubuntu, you can running the following command:

```bash
php composer.phar require mashape/unirest-php
```

Composer installs autoloader at `vendor/autoloader.php`. to include the library in your codeigniter project, open _config_ file on`application/config/config.php`and change the following code to:

```php
$config['composer_autoload'] = 'vendor/autoload.php';
```

or you can add manual to index.php file :

```php
require_once 'vendor/autoload.php';
```

#### Install from [source](https://github.com/Kong/unirest-php/releases)

Download the Unirest-PHP library from Github :

```bash
git clone git@github.com:Mashape/unirest-php.git 
```

Download the Unirest-PHP library manual on release page [here](https://github.com/Kong/unirest-php/releases). Extract the release in your codeigniter folder project.

Then include `Unirest.php` in your script at index.php or controller file:

```php
require_once '/path/to/unirest-php/src/Unirest.php';
```

{% hint style="warning" %}
 Install from source need to know the real path to the Unirest-PHP library.
{% endhint %}

### 3. StocKraken [HTTP Request](https://github.com/clickoding/http_request)

Download StocKraken HTTP Request Library from Github :

```bash
git clone https://github.com/clickoding/http_request.git
```

or you can chose other version on [release page Github here](https://github.com/clickoding/http_request/releases).

Extract the file zip and add to your codeigniter folder project.

you can load manual the library from controller by following this script :

```php
$this->load->library('http_req');
```

or you can add to autoload file at `application/config/autoload.php`:

```php
$autoload['libraries'] = array('Http_req' => 'httpku');
```

then you can load library on controller :

```php
$respon = $this->httpku->get('http://api.example.id/get_item');
echo $respon->raw_body;
```

and you ready to go.

## Usage /  Documentations

### Creating a Request

So you're probably wondering how using StocKraken HTTP Request makes creating requests in PHP easier, let's look at a working example:

```php
public function kategori() {

        $this->load->library('Http_req');

        $response = $this->http_req->get('https://api.bukalapak.com/v2/categories.json');

        print_r($response->code);        // HTTP Status code
        print_r($response->headers);     // Headers
        print_r($response->body);        // Body respon assoc

        echo '<br>';
        echo $response->raw_body;        // Unparsed body

}
```

or if you load Http\_req on autoload file and make alias `httpku`:

```php
public function kategori() {

        $response = $this->httpku->get('https://api.bukalapak.com/v2/categories.json');

        print_r($response->code);        // HTTP Status code
        print_r($response->headers);     // Headers
        print_r($response->body);        // Body respon assoc

        echo '<br>';
        echo $response->raw_body;        // Unparsed body

}
```

### Request Function

* Get Request

```php
$this->http_req->get($url, $headers = array(), $param = NULL);
```

* Post Request

```php
$this->http_req->post($url, $headers = array(), $body = NULL);
```

* Put Request

```php
$this->http_req->put($url, $headers = array(), $body = NULL);
```

* Patch Request

```php
$this->http_req->patch($url, $headers = array(), $body = NULL);
```

* Delete Request

```php
$this->http_req->delete($url, $headers = array(), $body = NULL);
```

* Custom Request - You can send a request with any [standard](http://www.iana.org/assignments/http-methods/http-methods.xhtml) or custom HTTP Method.

```php
$this->http_req->custom($http_method = 'get', $url, $headers = array(), $body = NULL);
```

#### Information

* `$url`  Endpoint, address, or uri to be acted upon and requested information from.
* `$headers` Request Headers as associative array or object, default is `array()`.
* `$body` Request Body as associative array or object, default `NULL`.
* `$http_method` custom HTTP Method, you can check list of `$http_method`or name method.

| NAME METHODS | [HTTP METHODS](http://www.iana.org/assignments/http-methods/http-methods.xhtml) |
| ---: | :--- |
| get | GET |
| head | HEAD |
| post | POST |
| put | PUT |
| delete | DELETE |
| connect | CONNECT |
| options | OPTIONS |
| trace | TRACE |
| baseline | BASELINE |
| link | LINK |
| unlink | UNLINK |
| merge | MERGE |
| basecontrol | BASELINE-CONTROL |
| mkactivity | MKACTIVITY |
| vercontrol | VERSION-CONTROL |
| report | REPORT |
| checkout | CHECKOUT |
| checkin | CHECKIN |
| uncheckout | UNCHECKOUT |
| mkworkspace | MKWORKSPACE |
| update | UPDATE |
| label | LABEL |
| orderpath | ORDERPATCH |
| acl | ACL |
| mkredirect | MKREDIRECTREF |
| upredirect | UPDATEREDIRECTREF |
| calendar | MKCALENDAR |
| propfind | PROPFIND |
| lock | LOCK |
| unlock | UNLOCK |
| proppath | PROPPATCH |
| mkcol | MKCOL |
| copy | COPY |
| move | MOVE |
| search | SEARCH |
| patch | PATCH |
| bind | BIND |
| unbind | UNBIND |
| rebind | REBIND |

### Headers

You cans simply add header on request function, look like example. But sometimes you need to add custom headers manual for all request.

```php
$this->http_req->set_Headers($headers);
```

#### Information

* `$headers` Request Headers as associative array or object.
* Example headers:

```php
$headers = array(
    'Accept' => 'application/json', 
    'Content-Type' => 'application/x-php-serialized'
);

$this->http_req->set_Headers($headers);

$this->http_req->get($url);    // headers $headers
$this->http_req->put($url);    // headers $headers
```

### Body

Set body makes you change all body request.

```php
$this->http_req->set_Body($body, $options = 'default');
```

#### Information

* `$body` Request Body as associative array or object or custom format.
* `$options` Options of type body you want to request, see the list of options body. Default is `default`.

#### Options Body

* `query` or `default`, Request Body as associative array or object.  


  ```php
  $body = array('foo' => 'bar', 'queen' => 'king');
  $this->http_req->set_Body($body);
  ```

* `json`, Request Body as associative array or object and will be convert to JSON Requests _\(`application/json`\)_.  


  ```php
  $body = array('foo' => 'bar', 'queen' => 'king');
  $this->http_req->set_Body($body, 'json');
  ```

  **Notes :**  


  * `Content-Type` headers will be automatically set to `application/json`
  * the data variable will be processed through [`json_encode`](http://php.net/manual/en/function.json-encode.php) with default values for arguments.
  * an error will be thrown if the [JSON Extension](http://php.net/manual/en/book.json.php) is not available. 

* `form`, Request Body as associative array or object and will be convert to Form Requests _\(`application/x-www-form-urlencoded`\)._  


  ```php
  $body = array('foo' => 'bar', 'queen' => 'king');
  $this->http_req->set_Body($body, 'form');
  ```

  **Notes :**  


  * `Content-Type` headers will be automatically set to `application/x-www-form-urlencoded`
  * the final data array will be processed through [`http_build_query`](http://php.net/manual/en/function.http-build-query.php) with default values for arguments. 

* `multipart`, Request Body as associative array or object and will be convert to Multipart Requests _\(`multipart/form-data`\)._  


  ```php
  $body = array('foo' => 'bar', 'queen' => 'king');
  $this->http_req->set_Body($body, 'multipart');
  ```

  **Notes :**  


  * `Content-Type` headers will be automatically set to `multipart/form-data`.
  * an auto-generated `--boundary` will be set. 

* `uploads`, Request Body as associative array or object and require key `body` and `files`. Key `body` is list of data body or parameter and key `files` is list of files and real path files. Data will be convert to Multipart File Upload.  


  ```php
  $body = array('foo' => 'bar', 'queen' => 'king');
  $files= array('images' => '/path/to/images/img.jpg');

  $uploads = array(
      'body' => $body,
      'files' => $files,
  );

  $this->http_req->set_Body($uploads, 'upload');
  ```

  If you wish to further customize the properties of files uploaded you can do so with the `get_File` function:



  ```php
  $mime_jpg = 'image/jpeg';
  $mime_png = 'image/png';
  $body = array(
      'foo'   => 'bar',
      'queen' => 'king',
      'images'=> $this->http_req->get_File('/path/to/images/img.jpg', $mime_jpg),
      'logo'  => $this->http_req->get_File('/path/to/logo.png', $mime_png),
  );

  $this->http_req->set_Body($body);
  ```

  
  **Notes :** we did not use the `multipart` options in this example, it is not needed when manually adding files.

### Timeout

You can set a custom timeout value for all request default \(in **seconds**\):

```php
$this->http_req->set_Timeout($seconds);
```

#### Information

* `$seconds`, Must be integer in seconds.

### **Authentication**

#### **Basic**

Otherwise, passing a username, password _\(optional\)_, defaults to Basic Authentication:

```php
$this->http_req->set_Auth($username, $password);
```

#### Mashape

First, if you are using [Mashape](https://www.mashape.com/) or [Kong](https://konghq.com/) Key:

```php
$this->http_req->set_Mashape('<key mashape or kong api key>');
```

then you can use `set_Auth` functions.

#### Custom / Proxy

Custom auth need third parameter. The third parameter, which is a bitmask, will StocKraken HTTP Request which HTTP authentication method\(s\) you want it to use for your proxy authentication.

If more than one bit is set, HTTP Request _\(at PHP's libcurl level\)_ will first query the site to see what authentication methods it supports and then pick the best one you allow it to use. _For some methods, this will induce an extra network round-trip._

```php
$this->http_req->set_Auth($username, $password, $curlmethod);
```

#### Information

* `$username`, must be string. If you use token then username can be token.
* `$password`, must be string. If you use token then just fill it with `''` .
* `$curlmethod`, HTTP authentication method for cURL. You can see the list of method.

#### List cURL HTTP Authentication Methods

| NAME METHOD | HTTP AUTH METHODS |
| ---: | :--- |
| basic | CURLAUTH\_BASIC |
| digest | CURLAUTH\_DIGEST |
| digest\_ie | CURLAUTH\_DIGEST\_IE |
| negotiate | CURLAUTH\_NEGOTIATE |
| ntlm | CURLAUTH\_NTLM |
| ntlm\_wb | CURLAUTH\_NTLM\_WB |
| any | CURLAUTH\_ANY |
| any\_safe | CURLAUTH\_ANYSAFE |
| only | CURLAUTH\_ONLY |

{% hint style="warning" %}
BEARER not support, because it won't support in the future PHP. You can use `set_Headers` for BEARER Token.
{% endhint %}

### Get File

Get file function is get file from path to upload with cURL file upload, here the code :

```php
$path  = 'path/real_path/txt/abc.txt';
$mime  = 'text/plain';

$image = $this->http_req->get_File($path, $mime);
```

This function is helpfully for upload file.

#### Information

* `$path`, Real path to the file.
* `$mime`, Mime types the files. See more [here](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types).

### Cookies

Set a cookie string to specify the contents of a cookie header. Multiple cookies are separated with a semicolon followed by a space \(e.g., "fruit=apple; color=red"\)

```php
$cookies = "fruit=apple; color=red";
$this->http_req->set_Cookies($cookies);
```

Set a cookie file path for enabling cookie reading and storing cookies across multiple sequence of requests.

```php
$pathcookiesfile = "/subcookies";
$this->http_req->set_Cookies($pathcookiesfile, 'file');
```

#### Information

* `$pathcookiesfile`, must be a correct path with write permission.

### **Custom JSON Decode Flags**

**StocKraken HTTP Request** uses PHP's [JSON Extension](http://php.net/manual/en/book.json.php) for automatically decoding JSON responses. sometime you may want to return associative arrays, limit the depth of recursion, or use any of the [customization flags](http://php.net/manual/en/json.constants.php).

To do so, simply set the desired options using the `set_JsonOpt` function:

```php
$assoc    = TRUE;    // default is FALSE
$rekusi   = 512;     // must be integer. Limit the depth of recursion
$options  = JSON_NUMERIC_CHECK & JSON_FORCE_OBJECT & JSON_UNESCAPED_SLASHES; // JSON constants
// for options you can ceck on customization flags
$this->http_req->set_JsonOpt($assoc, $rekusi, $options);
```

### Proxy

Set the proxy to use for the upcoming request.

```php
$this->http_req->set_Proxy($ip, $port, $tunneling, $proxytype);
```

#### Information

* `$ip`, must be string. IP proxy target. example `'10.10.23.200'`.
* `$port`, port of proxy. Default is 1080 - must be integer.
* `$tunneling`, Boolean \(TRUE/ FALSE\). Enable or disable tunneling.
* `$proxytype`, you can also set the proxy type to be one of `CURLPROXY_HTTP`, `CURLPROXY_HTTP_1_0`, `CURLPROXY_SOCKS4`, `CURLPROXY_SOCKS5`, `CURLPROXY_SOCKS4A`, and `CURLPROXY_SOCKS5_HOSTNAME`. Default is `CURLPROXY_HTTP`. _check the_ [_cURL docs_](http://curl.haxx.se/libcurl/c/CURLOPT_PROXYTYPE.html) _for more info_.

### **Default cURL Options**

You can set default [cURL options](http://php.net/manual/en/function.curl-setopt.php) that will be sent on every request:

```php
$options = array(
    CURLOPT_COOKIE => 'foo=bar',
);

$this->http_req->curl_options($options);
```

You can clear the default options anytime with:

```php
$this->http_req->curl_options('clear');
```

#### Information

* `$options`, must be array. for cURL option you can check the [cURL docs](https://curl.haxx.se/docs/).

### **SSL validation**

You can explicitly enable or disable SSL certificate validation when consuming an SSL protected endpoint:

```php
$this->http_req->ssl_validation(FALSE); // Disables SSL cert validation
```

{% hint style="info" %}
By default is `TRUE`.
{% endhint %}

### **Utility Methods**

```php
$this->http_req->utility(); // return curl_getinfo
$this->http_req->utility('info'); // return curl_getinfo
$this->http_req->utility('handle'); // returns internal cURL handle
```

## Bugs and Issues

For bugs, errors and issues you can send issues request at [GitHub clickoding](https://github.com/clickoding/http_request/issues).

