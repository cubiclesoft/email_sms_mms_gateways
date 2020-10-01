E-mail to SMS/MMS Gateways in JSON Format
=========================================

A simple repo containing a list of known e-mail to SMS, MMS, and Rich Messaging gateways in JSON format under a MIT or LGPL license.  If you want to add SMS or MMS support to your application but money/cost is an issue, this may be the answer you are looking for.  Basically, this is a giant list, sorted by country, of active gateways that transform e-mails into SMS/MMS messages on a mobile phone network.  It does have the downside of requiring the user to select their carrier, enter in their full phone number (usually with country code), and deal with their carrier's unique gateway issues (e.g. sometimes requires the number to be prefixed with '0', having to ask their carrier to enable e-mail to SMS for their account, etc).  While the biggest carriers tend to support e-mail to SMS/MMS, not every carrier does.

Carriers are constantly changing, so GitHub is a perfect fit for this sort of project.  Set up a cron job to download this project automatically or use it as a submodule in your own Git project.  If you know of any changes that need to be made, submit a pull request so that everyone benefits.

Features
--------

* Allows for free SMS/MMS integration into any application.
* Since it is in JSON format, it is programming language agnostic.
* Has a liberal open source license.  MIT or LGPL, your choice.
* Designed for relatively painless integration into your project.
* Sits on GitHub for all of that pull request and issue tracker goodness to easily submit changes and ideas respectively.

Useful Information
------------------

Using the file is pretty straight-forward.  Just load the file, JSON decode it (many languages offer native support), and then do something with it.

'sms_carriers' contains a list of carriers offering e-mail to SMS.  'mms_carriers' contains a list of carriers offering e-mail to MMS.  The latter list is much smaller.  Some of the SMS carriers support MMS, but don't count on it.

Each of the carriers are keyed off of a code for country or region (typically the ICANN TLD).  For example, 'us' is for 'United States'.  The 'countries' mapping can be used to map the code to a display name.  The key names are carefully chosen for maximum portability and no conflicts.  For example, if a web form contains a dropdown 'select' box, a 'us-at_and_t' value would be able to select the 'United States - AT&T' carrier.

The carriers are ordered as follows:  United States, Canada, countries sorted by their English name, and then weird stuff that doesn't fit in anywhere else.

Some carriers have more than one possible e-mail address.  Each carrier is listed in an array as ["Display name", "{number}@address.com", "{number}@address2.com"]  The first address listed is likely to work without any issue.  If you want to get fancy, give the user the option of which address to use.

On the application/server end of things, replace the string "number" with a user-supplied phone number.  Don't forget to do important stuff like sanitize the user's input so that only digits remain (no hyphens or other characters, just digits) and perform validation so users can't just enter any ol' e-mail address or otherwise break your desired system.  It is advisable to show the full e-mail address to the user that includes their mobile number so they can have the option to try it out first with their own e-mail provider to make sure it works.  A lot of mobile phone users don't know that e-mail to SMS even exists.

If possible, use a black hole e-mail address for the bouncebacks that will happen.  SMS/MMS gateways are not the greatest at handling error conditions.

Program your application to handle the case where a carrier ceases to exist and the entry vanishes or changes in the file.  It does happen.  Users may also change carriers and transfer their number to the new carrier.  Be as flexible as possible.

'lastupdated' contains the date of the last update of the file.  This exists so your application can figure out if it is working with stale information.

Mobile carriers don't actually necessarily need to own the network they are using.  These are known as Mobile Virtual Network Operators (MVNO).  An example is Tracfone, which uses multiple networks to deliver service to their customers - they negotiate the lowest possible rates from multiple providers such as AT&T, Sprint, T-Mobile, etc.  Straight Talk is another example of a MVNO, which may actually use Tracfone under the hood, but it gets confusing when multiple layers are involved.  The problem with MVNOs is that the user knows the brand name (e.g. Tracfone) but not their actual carrier (e.g. AT&T) until they go to do e-mail to SMS.  Each MVNO is constantly changing and bartering for the lowest prices to stay competitive.  As a result, the quality of this list is affected.  In general, the carrier most likely to be used is specified as the entry if the MVNO doesn't offer their own e-mail to SMS gateway.

Finally, this solution isn't going to work for everyone.  If you absolutely need SMS/MMS to work with the least hassle for your users, you will need to spend money.  There is currently no way around this.  Look for a 'GSM modem' if you need to go all out.  There are also web services like Twilio and Tropo available that do a lot of the hard work for you.  Each solution has upsides and downsides.

Sources
-------

The initial release of this project was a lot of manual data entry (yuck).  Wikipedia was the most helpful source - it was pretty easy to look at the history diffs to see what had changed.  Unfortunately, the article was deleted and the Internet now has no central source for the information.  Pull requests (or just open an issue in the tracker) are probably the only thing that will keep this repo current.  A couple other bits of information I found scattered around the Internet were also merged in.  A quick little command-line PHP script that checked the MX and A records of each domain helped identify and remove a number of obviously broken entries.

I'm pretty sure this is the most complete and functional list of this kind.  It is certainly the first time that this data has been massaged into a format suitable for use in most programming languages.  You're welcome.
