# finch-min
 Minimal Typescript Http Server

#### Features
finch is a simple framework for middleware HTTP services written in Typescript.   
Unlike other middleware systems, this code does not encapsulate the `request`( as
 `IncomingMessage` ) and `response` ( as `ServerResponse`) objects of the node itself.  
You can do whatever you want with native objects.

#### Compare with finch
Remove bundled middleware to keep it simple.

#### Install
` npm install finch-min`

#### Usage

```typescript
import {Finch, responseJson, responseStaticFiles} from "finch-min";

//instance a new finch for your app and name it;
let mike = new Finch();

//set the StaticFile app so mike can search and response files form it
mike.staticDir = "./static";

//Traditional way of using middleware
mike.use('/', (req, res, next) => {
    responseStaticFiles(res,"./static/index.html");
});
mike.use('/hello', (req, res, next) => {
    responseJson(res,{hello:'world'});
});

//start listening the port
mike.listen(3000);
```

#### Structure
The core is very simple and includes : 
* `Finch` : class;
    * `staticDir`
    * `listen(port: number)`
    * `use(handle: string, middleWare: middleWareFunction): void`
    * `all(middleWare: middleWareFunction):void`
* A set of `response` methods;
    * `responseJson(response: ServerResponse, msg: string | object)` 
    * `response404(response:ServerResponse) `
    * `response403(response:ServerResponse)`
    * `responseStaticFiles(res:ServerResponse, staticFilePath:string)`
    * `responseDownloadFile(res:ServerResponse, dfp:string, dfn?:string)`
    * `responseRedirect(response: ServerResponse, url: string)`
* `logger` : method;