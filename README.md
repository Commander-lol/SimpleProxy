SimpleProxy
===========

A simple, easily configurable node.js proxy built on top of node-http-proxy. 
Configuration is handled in two files: config/proxy.config.js and config/routes.config.js, although the former has limited uses at the present time. Simple logic routes the request to a given target based on the host header obtained from `request.headers.host`.

proxy.config.js options
=======================
The default proxy config object is as follows:
	{
		injectssl: false,
		server: {
			port: 8080
		}
	}

* `injectssl` : Whether or not to use the [ssl-root-cas](https://www.npmjs.org/package/ssl-root-cas) module for custom certificates
* `server` : Http Server configurations, which are currently just the port since the proxy doesn't explicitly bind to a host
	* `port` : The port on which to run SimpleProxy


routes.config.js options
========================
The routes config is a simple JSON object that defines how to handle each host. The key is the 'host', as it would appear in a header (sans protocol), and the value is the target, which can be one of three things.

* *String* : The host will be proxied to this address, which should include protocol
* *Object* : This will be passed as the `options` value to the `proxy.web(req, res, options)` call from [node-http-proxy](https://github.com/nodejitsu/node-http-proxy/blob/master/lib/http-proxy.js#L28-L51)
* *Function* : This function will be called with the arguments `req`, `res`, and `proxy`.

For examples of the different options, have a look at [the routes.config.js file]()

