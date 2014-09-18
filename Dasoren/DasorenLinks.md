## Site Links ##
#### Links to sites That I find interesting and want to note ####
---
### Coding ###
-  DNS
	- HTTP/DNS Redirect Rules with DNS and 200please.com 
	[http://redirect.200please.com/](http://redirect.200please.com/)
-  HTML
-  CSS
-  JavaScript
-  NodeJS
-  PHP
-  Java
-  DataBases
	-  Redis [http://redis.io/](http://redis.io/) -- [commands](http://redis.io/commands)
	-  MySQL [http://www.mysql.com/](http://www.mysql.com/) -- [Help/Commands](http://www.w3schools.com/sql/default.asp)
-  Learning
	-  W3Schools, learn basics of (html, css, php, mysql, js, xml, asp, and more) [http://w3schools.com/](http://www.w3schools.com/)
	- Code Academy learn (html, css, js, jquery, python, php, ruby) [http://codecademy.com/](http://www.codecademy.com/)
-  Other

---
### Tools ###
- DNS Propagation checker [https://www.whatsmydns.net/](https://www.whatsmydns.net/)
- WhOIS Checker [http://www.networksolutions.com/whois/index.jsp](http://www.networksolutions.com/whois/index.jsp)
- Website Performance Testing [http://www.webpagetest.org/](http://www.webpagetest.org/)

---
### Server admin ###
- IPTables
	- How To, Packet Filtering with IPTables [http://www.netfilter.org/documentation/HOWTO/packet-filtering-HOWTO-7.html](http://www.netfilter.org/documentation/HOWTO/packet-filtering-HOWTO-7.html)
	- Dropping Packets [http://stackoverflow.com/questions/23185001/dropping-packets-from-iptables](http://stackoverflow.com/questions/23185001/dropping-packets-from-iptables) 
		- Dropping packets FROM IP
		`iptables -s 123.456.78.90/32 -A INPUT -m statistic --mode random --probability 0.1 -j DROP`
		`iptables -s 123.456.78.90/32 -p tcp -m tcp -A INPUT -m statistic --mode random --probability 0.1 -j DROP`
		- Dropping Packers TO IP
		`iptables -d 123.456.78.90/32 -A OUTPUT -m statistic --mode random --probability 0.1 -j DROP`
		`iptables -d 123.456.78.90/32 -p tcp -m tcp -A OUTPUT -m statistic --mode random --probability 0.1 -j DROP`



---
### Email ###
- Mail Stache by mocx on FreeNode IRC [https://mailstache.io](https://mailstache.io)

---
### Games ###
- OSU, music game [http://osu.ppy.sh/](http://osu.ppy.sh/)

---
### Downloads ###

---
### Videos ###

---
### Music ###

---
### Pics ###

---
### OS ###
- Linux
	- Ubuntu
	- Mint
- Windows
	- Keyboard shortcuts [http://support.microsoft.com/kb/126449](http://support.microsoft.com/kb/126449)
- Mac

---
#### License ####
- Chose the right license, [http://choosealicense.com/licenses/](http://choosealicense.com/licenses/)
- Types

	Please see the sub-folder `licenses` for full text license files from the source sites. Or you can use the links under each type
	- GPL
		is the most widely used free software license and has a strong copyleft requirement. When distributing derived works, the source code of the work must be made available under the same license. There are multiple variants of the GPL, each with different requirements.
		- GNU GPL v2.0 [http://www.gnu.org/licenses/gpl-2.0.txt](http://www.gnu.org/licenses/gpl-2.0.txt)
		- GNU GPL v3.0 [http://www.gnu.org/licenses/gpl-3.0.txt](http://www.gnu.org/licenses/gpl-3.0.txt)
	- MIT
		a permissive license that is short and to the point. It lets people do anything with your code with proper attribution and without warranty.
		- MIT License [http://opensource.org/licenses/MIT](http://opensource.org/licenses/MIT)
	- Apache
		a permissive license that also provides an express grant of patent rights from contributors to users.
		- [http://choosealicense.com/licenses/apache-2.0/](http://choosealicense.com/licenses/apache-2.0/)
	- Mozilla
		Public License (MPL 2.0) is maintained by the Mozilla foundation. This license attempts to be a compromise between the permissive BSD license and the reciprocal GPL license.
		- Mozilla Public License v2.0 [https://www.mozilla.org/MPL/2.0/](https://www.mozilla.org/MPL/2.0/)
	- Artistic
		Heavily favored by the Perl community, the Artistic license requires that modified versions of the software do not prevent users from running the standard version.
		- Artistic License v2.0 [http://www.perlfoundation.org/attachment/legal/artistic-2_0.txt](http://www.perlfoundation.org/attachment/legal/artistic-2_0.txt)
	- No License
		You retain all rights and do not permit distribution, reproduction, or derivative works. You may grant some rights in cases where you publish your source code to a site that requires accepting terms of service. For example, publishing code in a public repository on GitHub requires that you allow others to view and fork your code.
		- No License [http://choosealicense.com/licenses/no-license/](http://choosealicense.com/licenses/no-license/)
	- Public Domain Dedication
		Because copyright is automatic in most countries, the Unlicense is a template to waive copyright interest in software you've written and dedicate it to the public domain. Use the Unlicense to opt out of copyright entirely. It also includes the no-warranty statement from the MIT/X11 license.
		- Unlicense [http://unlicense.org/UNLICENSE](http://unlicense.org/UNLICENSE)


The MIT License (MIT)

Copyright (c) 2014 Dasoren

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.