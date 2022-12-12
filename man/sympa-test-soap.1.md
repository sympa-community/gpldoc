---
title: 'sympa-test-soap(1)'
release: '6.2.71b.1'
---

# NAME

sympa-test-soap - Demo client for Sympa SOAP/HTTP API

# DESCRIPTION

`sympa test soap`
is a perl soap client for Sympa for TEST ONLY. Use it to illustrate how to
code access to features of Sympa soap server. Authentication can be done via
user/password or user cookie or as a trusted remote application

Usage: sympa test soap
\--service=&lt;a sympa service>
\--trusted\_application=&lt;app name>
\--trusted\_application\_password=&lt;password>
\--proxy\_vars=&lt;id=value,id2=value2>
\--service\_parameters=&lt;value1,value2,value3>
&lt;soap sympa server url>

OR usage: sympa test soap
\--user\_email=&lt;email>
\--user\_password=&lt;password>
\--session\_id=&lt;sessionid>
\--service=&lt;a sympa service>
\--service\_parameters=&lt;value1,value2,value3>
&lt;soap sympa server url>

OR usage: sympa test soap
\--cookie=&lt;sympauser cookie string>
&lt;soap sympa server url>

Example:
sympa test soap --cookie=sympauser=someone@cru.fr &lt;soap sympa server url> 

# HISTORY

`sympa_soap_client.pl` appeared on Sympa 4.0a.8.

Its function was moved to `sympa test soap` command line on Sympa 6.2.70.
