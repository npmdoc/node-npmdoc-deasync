# api documentation for  [deasync (v0.1.9)](https://github.com/abbr/deasync)  [![npm package](https://img.shields.io/npm/v/npmdoc-deasync.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-deasync) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-deasync.svg)](https://travis-ci.org/npmdoc/node-npmdoc-deasync)
#### Turns async function into sync via JavaScript wrapper of Node event loop

[![NPM](https://nodei.co/npm/deasync.png?downloads=true)](https://www.npmjs.com/package/deasync)

[![apidoc](https://npmdoc.github.io/node-npmdoc-deasync/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-deasync_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-deasync/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-deasync/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-deasync/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Vladimir Kurchatkin",
        "email": "vladimir.kurchatkin@gmail.com"
    },
    "bugs": {
        "url": "https://github.com/abbr/deasync/issues"
    },
    "contributors": [
        {
            "name": "Fred Wen",
            "email": "wenfred@gmail.com",
            "url": "https://github.com/abbr"
        }
    ],
    "dependencies": {
        "bindings": "~1.2.1",
        "nan": "^2.0.7"
    },
    "description": "Turns async function into sync via JavaScript wrapper of Node event loop",
    "devDependencies": {},
    "directories": {},
    "dist": {
        "shasum": "f58dd49fa63110c74bea8405a90a828be26d3a24",
        "tarball": "https://registry.npmjs.org/deasync/-/deasync-0.1.9.tgz"
    },
    "engines": {
        "node": ">=0.11.0"
    },
    "gitHead": "44fc8dca4ecf4ca39b264bdec296d3619a4aa0e3",
    "homepage": "https://github.com/abbr/deasync",
    "keywords": [
        "async",
        "sync",
        "sleep",
        "async wrapper"
    ],
    "license": "MIT",
    "main": "index.js",
    "maintainers": [
        {
            "name": "abbr",
            "email": "wenfred@gmail.com"
        }
    ],
    "name": "deasync",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+https://github.com/abbr/deasync.git"
    },
    "scripts": {
        "install": "node ./build.js"
    },
    "version": "0.1.9"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module deasync](#apidoc.module.deasync)
1.  [function <span class="apidocSignatureSpan">deasync.</span>loopWhile (pred)](#apidoc.element.deasync.loopWhile)
1.  [function <span class="apidocSignatureSpan">deasync.</span>runLoopOnce ()](#apidoc.element.deasync.runLoopOnce)
1.  [function <span class="apidocSignatureSpan">deasync.</span>sleep ()](#apidoc.element.deasync.sleep)



# <a name="apidoc.module.deasync"></a>[module deasync](#apidoc.module.deasync)

#### <a name="apidoc.element.deasync.loopWhile"></a>[function <span class="apidocSignatureSpan">deasync.</span>loopWhile (pred)](#apidoc.element.deasync.loopWhile)
- description and source-code
```javascript
loopWhile = function (pred){
	  while(pred()){
		process._tickDomainCallback();
		if(pred()) binding.run();
	  }
	}
```
- example usage
```shell
...
'''javascript
var done = false;
var data;
asyncFunction(p1,function cb(res){
    data = res;
    done = true;
});
require('deasync').loopWhile(function(){return !done;});
// data is now populated
'''

* Sleep (a wrapper of setTimeout)

'''javascript
function SyncFunction(){
...
```

#### <a name="apidoc.element.deasync.runLoopOnce"></a>[function <span class="apidocSignatureSpan">deasync.</span>runLoopOnce ()](#apidoc.element.deasync.runLoopOnce)
- description and source-code
```javascript
runLoopOnce = function (){
		process._tickDomainCallback();
		binding.run();
	}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.deasync.sleep"></a>[function <span class="apidocSignatureSpan">deasync.</span>sleep ()](#apidoc.element.deasync.sleep)
- description and source-code
```javascript
sleep = function () {
			var done = false;
			var args = Array.prototype.slice.apply(arguments).concat(cb);
			var err;
			var res;

			fn.apply(this, args);
			module.exports.loopWhile(function(){return !done;});
			if (err)
				throw err;

			return res;

			function cb(e, r) {
				err = e;
				res = r;
				done = true;		
			}
		}
```
- example usage
```shell
...
'''javascript
function SyncFunction(){
  var ret;
  setTimeout(function(){
      ret = "hello";
  },3000);
  while(ret === undefined) {
    require('deasync').sleep(100);
  }
  // returns hello with sleep; undefined without
  return ret;
}
'''

## Installation
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
