# Extension:SimpleFeed

This extension outputs the contents of an RSS feed. It is very customisable. As a result, no editing of the PHP source is required as everything is done in the wiki page.

## Installation

 1. cd ./extensions/
 2. git clone https://github.com/dennisroczek/simplefeed
 3. set correct write permissions using chmod (www-user, or equivalent, should be allowed to write). Permissions are usually 755, 775 or 777. See setting permissions for cache directory
 4. Add require_once "$IP/extensions/SimpleFeed.php"; to LocalSettings.php
 5. If you are in a corporate environment, check out any proxy servers or firewalls.

## Usage
### Simple Method ###
The url address must be between the <feed>[...]</feed> tags. For example:
<feed>http://newsrss.bbc.co.uk/rss/newsonline_uk_edition/front_page/rss.xml<feed>

### Customized Method ###
The url address must be between the <feed>[...]</feed> tags. For example:
    <feed url="http://newsrss.bbc.co.uk/rss/newsonline_uk_edition/front_page/rss.xml">
    == [{PERMALINK} {TITLE}] ==
    '''{DATE}, by {AUTHOR}'''
    {DESCRIPTION}
    </feed>
This will pull the BBC News feed and output five posts. For every post, it will output the data between the feed tags, replacing {PERMALINK}, {TITLE}, {DATE}, {AUTHOR} and {DESCRIPTION} with the appropriate information.


## Customization

You can customize the output by using the following:
### url
The URL of the feed. This argument is not optional. 
### entries
The number of post entries to output. This defaults to 5, but can be any number. 0 is unlimited.
### type
If this is set to "planet" then the post title and author will be retrieved from the title. For example, a post in a planet/aggregator could have a title "Joe Bloggs: MediaWiki is great". If type="planet" is set, then {TITLE} will become "Mediawiki is great", and {AUTHOR} will become "Joe Bloggs".
### date
The format of the date to output. This conforms to PHP's date function syntax. This defaults to j F Y (E.g. 3 March 2007).
### sort
If you specify sort="asc" then the feeds will be displayed in revers order. 

## Further examples
Using an aggregator's feed

	<feed url="http://planet.debian.org/rss20.xml" type="planet">
	== [{PERMALINK} {TITLE}] == 
	'''{DATE}, by {AUTHOR}''' {DESCRIPTION}
	</feed>

This will remove the author's name from the title of the post, and setting its value to {AUTHOR}.

## Changing the date format
    <feed url="http://planet.debian.org/rss20.xml" date="h:i:s d/m/y T">...
Changes the date format to, in this example, "23:20:04 24/03/2007 GMT".

## Parameters
Line 31: $simplepie_path - string: Path to simplepie.inc, including leading forward slash. For example:
		  $simplepie_path = 'extensions/';

## Todo
The following feature(s) to be added:
1. Check whether the URL given is a correct address. If SimplePie can't read it, output something.
2. Clean up the regular expressions.
