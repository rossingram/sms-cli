
<h1>Send a Twilio SMS from the Shell</h1>
<p>
	The <a href='/packages/labs/code/bash/twilio-sms'>twilio-sms</a> bash script will send an SMS to one or more phone numbers provided on the command line, using content read from STDIN!  It can practically be used as a drop-in replacement for mail in some instances.
</p>
<p>
	The script can read configuration parameters, such as your Twilio AccountSid, AuthToken and CallerID from the command line, or more preferably from a config file.  You can provide the path to a config file in the arguments, or the default ~/.twiliorc will be tried. 
</p>
<p>
	Additionally, you can provide one or more phone numbers in a single invocation of the script, and all the numbers will be texted.
</p>
<div class='shell-example' style='clear: both'>
	Usage: twilio-sms [-v] [-c configfile] [-d callerid] [-u accountsid] [-p authtoken] number [number[number[...]]]
</div>

<h2>Installation</h2>
<ol>
<li><a href='/packages/labs/code/bash/twilio-sms'>Download</a> the twilio-sms bash script and put it somewhere in your path.</li>
<li>chmod 775 twilio-sms</li>
<li><em>Optional:</em> Setup a default <a href='#config'>config file</a> in ~/.twiliorc or a location of your choice</li>
</ol>

<h2>Example Usage</h2>
<div class='shell-example'>
	echo "Hi There" | ./twilio-sms 415-555-1212
</div>
Will text "Hi There" to 415-555-1212.

<div class='shell-example'>
	echo "Hi There" | ./twilio-sms 415-555-1212 415-555-1313
</div>
Will text "Hi There" to 415-555-1212 and 415-555-1313.

<div class='shell-example'>
	echo "Hi There" | ./twilio-sms -u AC12345... -p d45bd.. -d 555-867-5309 415-555-1212
</div>
Will text "Hi There" to 415-555-1212, and the SMS will come from your Twilio phone number 555-867-5309, and the AccountSid and AuthToken will be used to authenticate with Twilio's API.

<div class='shell-example'>
	echo "Hi There" | ./twilio-sms -c /etc/twilio.conf 415-555-1212
</div>
Will text "Hi There" to 415-555-1212 using AccountSid, AuthToken and CallerId parameters read from /etc/twilio.conf.

<div class='shell-example'>
	echo "Hi There" | ./twilio-sms -v 415-555-1212
</div>
Will text "Hi There" to 415-555-1212 running in verbose mode, meaning it outputs to STDOUT the XML response received from the Twilio REST API.

<h2 id="config">Config File</h2>
<p>The config file consists of bash variable declarations, as name=value pairs, each on one line. The file may contain any of the following parameters that will be used as defaults and therefore, don't need to be specified on the command line:</p>
<table class='doc-table' width='500px'>
	<tr>
		<th>Attribute Name</th>
		<th>Description</th>
	</tr>
	<tr>
		<td>ACCOUNTSID</td>
		<td>Your Twilio AccountSid.  For example: AC1234567890</td>
	</tr>
	<tr>
		<td>AUTHTOKEN</td>
		<td>Your Twilio AuthToken.  For example: dk49dkdcb3948abd</td>
	</tr>
	<tr>
		<td>CALLERID</td>
		<td>A valid Twilio phone number configured for your account. Note: must be a phone number purchased from Twilio, a validated caller-id will not work.  For example: 555-867-5309</td>
	</tr>
</table>

<h3>Example Config File</h3>
<div class='shell-example'>
	<pre>
ACCOUNTSID=AC1234567890
AUTHTOKEN=dk49dkdcb3948abd
CALLERID=555-867-5309
	</pre>
</div>