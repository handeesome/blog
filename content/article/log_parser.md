---
title: "Log_parser"
date: 2020-11-16T13:12:11+01:00
draft: true

categories: []
tags: []
author: ""
---

## Access and Error Log Parser into Segments Using apeche-log-parser

### Example access log format
'''
LogFormat "%h %l %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-agent}i\""
'''
different log formats: https://httpd.apache.org/docs/2.4/logs.html 
    '''
        127.0.0.1 - frank [10/Oct/2000:13:55:36 -0700] "GET /apache_pb.gif HTTP/1.0" 200 2326 "http://www.example.com/start.html" "Mozilla/4.08 [en] (Win98; I ;Nav)"
        '''
    
#### python code for printing respective items of one line in log
'''python
import apache_log_parser

line_parser = apache_log_parser.make_parser("%h %l %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-agent}i\"")
log_line_data = line_parser('10.222.130.214 - - [10/Nov/2020:19:27:36 +0100] "GET /~cdu/index_login.php HTTP/1.1" 200 692 "http://clabsql.clamv.jacobs-university.de/~cdu/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/86.0.4240.183 Safari/537.36"')

from pprint import pprint
pprint(log_line_data)
'''

#### output
![output](/static/img/access_log_output.png)


#### Each part of this log entry is described below.

#### 127.0.0.1 (%h)
This is the IP address of the client (remote host) which made the request to the server. If HostnameLookups is set to On, then the server will try to determine the hostname and log it in place of the IP address. However, this configuration is not recommended since it can significantly slow the server. Instead, it is best to use a log post-processor such as logresolve to determine the hostnames. The IP address reported here is not necessarily the address of the machine at which the user is sitting. If a proxy server exists between the user and the server, this address will be the address of the proxy, rather than the originating machine.
#### \- (%l)
The "hyphen" in the output indicates that the requested piece of information is not available. In this case, the information that is not available is the RFC 1413 identity of the client determined by identd on the clients machine. This information is highly unreliable and should almost never be used except on tightly controlled internal networks. Apache httpd will not even attempt to determine this information unless IdentityCheck is set to On.
#### frank (%u)
This is the userid of the person requesting the document as determined by HTTP authentication. The same value is typically provided to CGI scripts in the REMOTE_USER environment variable. If the status code for the request (see below) is 401, then this value should not be trusted because the user is not yet authenticated. If the document is not password protected, this part will be "\-" just like the previous one.
#### [10/Oct/2000:13:55:36 -0700] (%t)
The time that the request was received. The format is:

[day/month/year:hour:minute:second zone]
day = 2\*digit
month = 3\*letter
year = 4\*digit
hour = 2\*digit
minute = 2\*digit
second = 2\*digit
zone = (\`+\' | \`-\') 4\*digit

It is possible to have the time displayed in another format by specifying %{format}t in the log format string, where format is either as in strftime(3) from the C standard library, or one of the supported special tokens. For details see the mod_log_config format strings.

#### "GET /apache_pb.gif HTTP/1.0" (\"%r\")
The request line from the client is given in double quotes. The request line contains a great deal of useful information. First, the method used by the client is GET. Second, the client requested the resource /apache_pb.gif, and third, the client used the protocol HTTP/1.0. It is also possible to log one or more parts of the request line independently. For example, the format string "%m %U%q %H" will log the method, path, query-string, and protocol, resulting in exactly the same output as "%r".
#### 200 (%>s)
This is the status code that the server sends back to the client. This information is very valuable, because it reveals whether the request resulted in a successful response (codes beginning in 2), a redirection (codes beginning in 3), an error caused by the client (codes beginning in 4), or an error in the server (codes beginning in 5). The full list of possible status codes can be found in the HTTP specification (RFC2616 section 10).
#### 2326 (%b)
The last part indicates the size of the object returned to the client, not including the response headers. If no content was returned to the client, this value will be "-". To log "0" for no content, use %B instead.

#### "http://www.example.com/start.html" (\"%{Referer}i\")
The "Referer" (sic) HTTP request header. This gives the site that the client reports having been referred from. (This should be the page that links to or includes /apache_pb.gif).
#### "Mozilla/4.08 [en] (Win98; I ;Nav)" (\"%{User-agent}i\")
The User-Agent HTTP request header. This is the identifying information that the client browser reports about itself.

## Generate Access and Error Logs into html

'''bash
goaccess new_access_log -o access.html --log-format=COMBINED

goaccess new_error_log --log-format='[%^ %d %t.%^ %^] [%^] [%^] [%^ %h:%^] %^: %U, %^: %R' --time-format=%T --date-format='%b %d' --http-protocol=no --http-method=no -o error.html
...

####

#### error log format
![error fomat](/static/img/error_log_format.png)
