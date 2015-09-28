# Request

```
https://api.flickr.com/services/rest/?method=flickr.test.echo&name=value
https://www.flickr.com/services/rest/?method=flickr.test.echo&format=rest&foo=bar&api_key=b6386c139dfa88173692ab96594628c5
https://www.flickr.com/services/rest/?method=flickr.test.echo&format=php_serial&foo=bar&api_key=b6386c139dfa88173692ab96594628c5
```

# Response

## Structure

XML

```xml
<outer>
	<photo id="1" />
	<photo id="2" />
</outer>
```

```xml
<?xml version="1.0" encoding="utf-8" ?>
<rsp stat="ok">
	[xml-payload-here]
</rsp>
```

```xml
<?xml version="1.0" encoding="utf-8" ?>
<rsp stat="fail">
	<err code="[error-code]" msg="[error-message]" />
</rsp>
```

JSON

```json
{
	"outer": {
		"photo": [
			{
				"id": "1"
			},
			{
				"id": "2"
			}
		]
	}
}
```

PHP Serialized:

```php
a:5:{s:6:"method";a:1:{s:8:"_content";s:16:"flickr.test.echo";}s:6:"format";a:1:{s:8:"_content";s:10:"php_serial";}s:3:"foo";a:1:{s:8:"_content";s:3:"bar";}s:7:"api_key";a:1:{s:8:"_content";s:32:"b6386c139dfa88173692ab96594628c5";}s:4:"stat";s:2:"ok";}
```
