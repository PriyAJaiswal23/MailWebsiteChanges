# MailWebsiteChanges

Python script to keep track of website changes; sends email notifications on updates and/or also provides an RSS feed

To specify which parts of a website should be monitored, <b>both XPath selectors</b> (e.g. "//h1") <b>and regular expressions can be used</b>.

## Configuration
Configuration can be done by creating a <code>config.py</code> file (just place this file in the program folder):
Some examples:

### Website definitions
<pre>
<code>
 # short name | URI | content type | XPath | regular expression | encoding

 sites = [['shortname1', 'http://www.mywebsite1.com/info', 'html', '//h1', '', 'utf-8'],
          ['shortname2', 'http://www.mywebsite2.com/info', 'xml', '//*[contains(concat(\' \', normalize-space(@class), \' \'), \'news-list-container\')]', '', 'utf-8'],
          ['shortname3', 'http://www.mywebsite3.com', 'text', '', 'Version\"\:\d*\.\d*', 'utf-8']
         ]
</code>
</pre>

<em>SelectorTest.py</em> might be useful in order to test the definitions before integrating them into the config file.

### Mail settings
<pre>
<code>
 subjectPostfix = 'A website has been updated!'
 sender = 'me@mymail.com'
 smtptlshost = 'mysmtpprovider.com'
 smtptlsport = 587
 smtptlsusername = sender
 smtptlspwd = 'mypassword'
 receiver = 'me2@mymail.com'

 os.chdir('/path/to/working/directory')
</code>
</pre>

If <em>receiver</em> is empty, no mail will be sent.

### Cron job
To setup a job that periodically runs the script, simply attach something like this to your /etc/crontab:
<pre>
<code>
0 22	* * *	root	/usr/bin/python /path/to/MailWebsiteChanges/MailWebsiteChanges.py
</code>
</pre>
This will run the script once a day at 10pm.

### RSS Feeds
If you prefer to use the RSS feature, you just have to specify the path of the feed file which should be generated by the script (e.g., rssfile = 'feed.xml') and then point your webserver (e.g., <a href="http://twistedmatrix.com/trac/wiki/TwistedWeb">TwistedWeb</a>) to that file.


## Requirements
Requires <a href="http://lxml.de/">lxml</a>.

