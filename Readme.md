
# jsonp

A simple JSONP implementation.

## Installation

Install for node.js or browserify using `npm`:

``` bash
$ npm install jsonp
```

Install for component(1) using `component`:

``` bash
$ component install LearnBoost/jsonp
```

Install for browser using `bower`:

``` bash
$ bower install jsonp
```

## API

### jsonp(url, opts, fn)

- `url` (`String`) （字符串URL获取）
- `opts` (`Object`), 可选
  - `param` (`String`) 指定回调的查询字符串参数的名称
     callback （默认为回调）
  - `timeout` (`Number`) 后超时错误是如何发出长。
     disable (零禁用) default (默认为60000)
  - `prefix` (`String`) 为全局JSONP回调函数响应前缀 （默认为__jp）
  - `name` (`String`) 为全局JSONP回调函数名称（默认`prefix`+递增的计数器）
- `fn` 回调函数

The callback is called with `err, data` parameters.

If it times out, the `err` will be an `Error` object whose `message` is
`Timeout`.

Returns a function that, when called, will cancel the in-progress jsonp request
(`fn` won't be called).

### jsonp的实现

 `//封装jsonp`

 `import orginJSONP from "jsonp"`

	export default  function jsonp(url,data,option) {
	  url+=(url.indexOf('?')<0?'?':'&')+param(data);
	  return new Promise((resolve,reject)=>{
	    orginJSONP(url,option,(err,data)=>{
	      if(!err){
	        resolve(data);
	      }else {
	        reject(err);
	      }
	    })
	  })
	}

	function param(data) {
	  let url='';
	  for(var k in data){
	    let value=data[k]!==undefined?data[k]:'';
	    //拼接地址栏路径
	    url+=`&${k}=${encodeURIComponent(value)}`;
	  }
	  return url?url.substring(1):'';
	}

