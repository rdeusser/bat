# httplib
httplib is an libs help you to curl remote url.

# How to use?

## GET
you can use Get to crawl data.

	import "github.com/astaxie/bat/httplib"
	
	str, err := httplib.Get("http://bat.me/").String()
	if err != nil {
        	// error
	}
	fmt.Println(str)
	
## POST
POST data to remote url

	req := httplib.Post("http://bat.me/")
	req.Param("username","astaxie")
	req.Param("password","123456")
	str, err := req.String()
	if err != nil {
        	// error
	}
	fmt.Println(str)

## Set timeout

The default timeout is `60` seconds, function prototype:

	SetTimeout(connectTimeout, readWriteTimeout time.Duration)

Exmaple:

	// GET
	httplib.Get("http://bat.me/").SetTimeout(100 * time.Second, 30 * time.Second)
	
	// POST
	httplib.Post("http://bat.me/").SetTimeout(100 * time.Second, 30 * time.Second)


## Debug

If you want to debug the request info, set the debug on

	httplib.Get("http://bat.me/").Debug(true)
	
## Set HTTP Basic Auth

	str, err := Get("http://bat.me/").SetBasicAuth("user", "passwd").String()
	if err != nil {
        	// error
	}
	fmt.Println(str)
	
## Set HTTPS

If request url is https, You can set the client support TSL:

	httplib.SetTLSClientConfig(&tls.Config{InsecureSkipVerify: true})
	
More info about the `tls.Config` please visit http://golang.org/pkg/crypto/tls/#Config	

## Set HTTP Version

some servers need to specify the protocol version of HTTP

	httplib.Get("http://bat.me/").SetProtocolVersion("HTTP/1.1")
	
## Set Cookie

some http request need setcookie. So set it like this:

	cookie := &http.Cookie{}
	cookie.Name = "username"
	cookie.Value  = "astaxie"
	httplib.Get("http://bat.me/").SetCookie(cookie)

## Upload file

httplib support mutil file upload, use `req.PostFile()`

	req := httplib.Post("http://bat.me/")
	req.Param("username","astaxie")
	req.PostFile("uploadfile1", "httplib.pdf")
	str, err := req.String()
	if err != nil {
        	// error
	}
	fmt.Println(str)


See godoc for further documentation and examples.

* [godoc.org/github.com/astaxie/bat/httplib](https://godoc.org/github.com/astaxie/bat/httplib)
