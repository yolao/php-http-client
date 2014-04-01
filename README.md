# PHP-Http-Class
- Http class used to sending request and get response like a browser.
- Use 2 functions: cURL, fsockopen, so you can use this class, "curl" **WITHOUT CURL** extension installed
- Supports POST (fields, raw data), file uploading, GET, PUT, etc..

**Note**: _fsockopen_ is faster also it is default.

* Author:     Phan Thanh Cong <ptcong90@gmail.com>
* Copyright:  2011-2014 Phan Thanh Cong.
* License:    http://www.opensource.org/licenses/mit-license.php  MIT License
* Version:    2.5.3

## Change logs
#### Version 2.5.3: Apr 1, 2014
* Add new method setFollowRedirect() to follow redirect
* Add new method getResponseArrayCookies() to get all cookies by array [name => [info], name2 => [info]]
* Fixed a bug
* Change all properties to protected (need use set* methods to change the properties)

#### Version 2.5: Mar 07, 2014
* Change class name to \ChipVN\Http\Request
* Most clean and clear
* Supports composer
* Add new method setHttpVersion() to change HTTP protocol version

#### Version 2.4: Jul 25, 2013
* Require PHP 5.3 or newer
* Change two static class methods (readBinary, mimeTye) to protected instance method

#### Version 2.3.4: Feb 20, 2013
* Fixed parse headers (typo)

#### Version 2.3.3: Nov 5, 2012
* Re-struct, something edited

#### Version 2.3.2: June 12, 2012
* Add some methods

#### Version 2.3.1: Mar 30, 2012
* Fixed some bugs to work well with PHP 5.3 (E_NOTICE default is enabled)

#### Version 2.3: Feb 2, 2012
* Update for picasa API

#### Version 2.2: Jan 1, 2012
* Support raw data for posting (upload image to picasa)

#### Version 2.1: Dec 23, 2011
* Fixed some bugs

#### Version 2.0: Jun 26, 2011
* Rewrite class to easy use
* Fixed some bugs

#### Version 1.2: April 19, 2011
* Mime-type bug on upload file fixed 

#### Version 1.1:
* Supports upload multiple files
* Fixed some bugs

#### Version 1.0:
* Supports send a basic request
* Proxy (only useCurl)
* Supports file uploading

## Usage

Add require `"ptcong/php-http-class": "2.5.*@dev"` to _composer.json_ and run `composer update` if you use composer

### Read web content:
	$http = new \ChipVN\Http\Request;
	$http->setTarget("http://www.yourwebsite.com/");
	$http->execute();
	print_r($http->getResponseHeaders());
	echo $http->getResponseText();
	
### Submit form:
	$http = new \ChipVN\Http\Request;
	$http->setTarget("http://www.yourwebsite.com/");
	$http->setParam(array("fieldname"=> $value)); 
	$http->setMethod('POST');
	$http->execute();
	echo $http->getResponseText();
	
### Using Proxy: only useCurl
	$http = new \ChipVN\Http\Request;
	$http->useCurl(true);
	$http->setTarget("http://www.yourwebsite.com/");
	$http->setProxy('proxy_ip:proxy_port');
	$http->execute();
	echo $http->getResponseText();

### Upload file:
	$filePath = getcwd().'/abc.jpg';
	$http = new \ChipVN\Http\Request;
	$http->setTarget("http://www.yourwebsite.com/");
	$http->setSubmitMultipart();
	$http->setParam(array('fileupload'=>"@$filePath"));
	$http->execute();
	print_r($http->getResponseHeaders());
	echo $http->getResponseText();