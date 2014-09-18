## HTTP DNS Redirect ##
[200please.com](http://redirect.200please.com/)
### Why HTTP 301?

If you've moved your site to a new domain,
it's very important to redirect your existing users and search engine to your new URL. 
Your existing users should still be ok with other 
[HTTP 3xx](http://en.wikipedia.org/wiki/HTTP_status_code#3xx_Redirection) 
redirection or even 
[CNAME](http://en.wikipedia.org/wiki/Cname) 
alias, but search engines don't.
Here is an 
[article](http://support.google.com/webmasters/bin/answer.py?hl=en&answer=83106) 
from Google explains why it is important to use 
[HTTP 301](http://en.wikipedia.org/wiki/HTTP_301) 
to redirect.

We try to provide the easiest way to setup a HTTP 301 redirection. 
No registration, no installation, not even login to a web server.
All you need to do is to **update two DNS records**.

### Steps with example

Let's say we want to redirect all URLs from 
<span style="color: blue;text-decoration: underline;">http://blog.example.org</span> to 
<span style="color: blue;text-decoration: underline;">http://www.exampleblog.org/blog/</span>.
First we need to login to DNS hosting console:

1.  Create an **A Record** of the domain / sub-domain you want to redirect with address of:

	<pre>50.112.126.117</pre>
	in this case we will need to make sure **A Record** _blog.example.org_ is pointing to **50.112.126.117**

2.  Create a TXT record (the **redirect instruction**) of the domain / sub-domain you want to redirect, with value of:

	<pre>200please.redirect=[Destination URL]</pre>
	Note that the [Destination URL] is not merely a host name, it should be **protocol://hostname:port/path**
	In our case, **TXT** record _blog.example.org_ shall having a value of **200please.redirect=http://www.exampleblog.org/blog/**

### Refresh and Verify your settings

Once you created / updated above DNS settings, you can input your from hostname (in above example _blog.example.org_) to make sure the settings are correct. 

***Does not work***
<div class="well form-inline">
<input id="refresh_domain" type="text" class="input-large" placeholder="hostname eg, grepnetstat.com">
<button id="refresh_btn" class="btn">Start</button>
</div>
<div id="refresh_output" class="alert alert-block hide"></div>***Does not work***

### Update / Cancel Redirection

*   Redirection will be cached in order to have a better performance.
*   If you want to change your redirection, you will need to use above **refresh / verify** tool to refresh our cache once you have updated **TXT** record (created in above **Step 2**).
*   If you do not want to use our redirection anymore. Simply remove the **A Record** (created in above **Step 1**). You can keep the TXT record for future use. No side effect, promise.

### Alternatives

   There are several other options to setup a redirection.

*   **Use your own HTTP Server**

	You can always use your own HTTP server to perform HTTP 301 redirect.
	Nowadays all popular web servers should support HTTP redirection.
	This is exactly the same way as we do.    			It may take couple of hours to setup and verify if you are not familiar with them.

	You can use our free [HTTP monitoring tool](http://www.200please.com) to make sure you web server are using 301 redirect correctly.
*   **DNS / Web hosting provider**

	Some DNS / Web hosting company provides this feature to use their web server to redirect too.
	The setup will be easier compared with the first alternative. This is also working in the same way.

	Again, you can use our [HTTP monitoring tool](http://www.200please.com) to verify redirection.
*   **Use Google App to redirect naked domain**

    We have to admit, though it brings us great shame to say: Google's servers are usually faster than ours.

    Click [here](http://www.200please.com/?url=http%3A%2F%2F200plz.com) to check performance difference when redirecting <a>200plz.com</a>.
    Google is used to redirect from <a>200plz.com</a> to <a>www.200plz.com</a>, and our server will redirect from <a>www.200plz.com</a> to <a>www.200please.com</a>

    However, there are several limitations for this approach:

    *   Only naked domain can be redirected. ie, you can only redirect from <a>example.com</a>, but not <a>www.example.com</a>
    *   The destination has to be the root of a subdomain. ie, you can only redirect to <a>www.example.com</a>, but not <a>www.othersite.com</a> or <a>www.example.com/path?param=p1</a>
    Read [this page](http://support.google.com/a/bin/answer.py?hl=en&answer=2518373) for more setup details.

*   **Create DNS records to map new domains to the same server <span style="color:red;">Not recommended</span>**

	You can create CNAME / A records to make new domain resolves to the existing servers. But just don't do this. A web site can NEVER be moved in this way.    Your users will still visit your old site and search engine will still crawl you old pages.
	Your new site will be treated as merely another site with duplicated content.

### Miscellaneous

*   Google's [Best Practices](http://googlewebmastercentral.blogspot.hk/2008/04/best-practices-when-moving-your-site.html) When Moving Your Site
*   Feel free to [email us](mailto:hello@200please.com), if it still doesn't work, or other issues you encountered when moving your site. We are more than happy to help!