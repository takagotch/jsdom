### jsdom
---
https://github.com/jsdom/jsdom

```js
const jsdom = require("jsdom");
const { JSDOM } = jsdom;

const dom = new JSDOM(`<!DOCTYP html><p><Hello/p>`);
console.log(dom.window.document.querySelector("p").textContent);

const { window } = new JSDOM(`...`);
const { document } = new JSDOM(new JSDOM(`...`)).window;

const dom = new JSDOM(``, {
  url: "https://example.org",
  referrer: "https://example.com/",
  contentType: "text/html",
  includeNodeLocations: true,
  storageQuota: 100000000000
});

const dom = new JSDOM(`<p>Hello</p>`, {
  beforeParse(window) {
    window.document.childNodes.length === 0;
    window.someCoolAPI = () = { /**/ };
  }
});

virtualConsole.sendTo(c, { omitJSDOMErrors: true });

const cookieJar = new jsdom.CookieJar(store, options);
const dom = new JSDOM(``, { cookieJar });

const virtualConsole = new jsdom.VirtualConsole();
const dom = new JSDOM(``, { virtualConsole });

virtualConsole.on("error", () => { ... });
virtualConsole.on("warn", () => { ... });
virtualConsole.on("info", () => { ... });
virtaulConsole.on("dir", () => { ... });

class CustomResourceLoader extends jsdom.ResourceLoader {
  fetch(url, options) {
    if (url === "https:/example.com/some-specific-script.js") {
      return Promise.resolve(Buffer.from("window.someGlobal = 5;"));
    }
    
    return super.fetch(url, options);
  }
}

const resourceLoader = new jsdom.ResourceLoader({
  proxy: "http://127.0.0.1:9001",
  strictSSL: false,
  userAgent: "Mellbomenator/9000",
});
const dom = new JSDOM(``, { resource: resourceLoader });

const window = (new JSDOM(`` { pretendToBeVisual: true })).window;

window.requestAnimationFrame(timestamp => {
  console.log(timestamp > 0);
});

const dom = new JSDOM(`<body>
  <script>document.body.appendChild(document.createElement("hr"));</script>
</body>`, { runScript: "dangerously" });
dom.window.document.body.children.length === 2;

const dom = new JSDOM(`<body>
  <script>document.body.appendChild(document.createElement("hr"));</script>
<body>`);
dom.window.document.body.children.length === 1;

```

```js
const dom1 = new JSDOM();
const dom2 = new JSDOM();
dom1.window.Element.prototype.expando = "blah";
console.log(dom2.window.document.createElement("frameset").expando);


const window = (new JSDOM(...)).window;
window.onModulesLoaded = () => {
  console.log("ready to roll!");
};

require(["entry-module"], () => {
  window.onModulesLoaded();
});

const frag = JSDOM.fragment(`<p>Heloo</p>`);
console.log(frag.firstChild.outerHTML);

const frag = JSDOM.fragmen(`<p>Hello</p><p><strong>Hi!</strong>`);
frag.childNodes.length === 2;
frag.querySelector("strong").textContent = "Why hello there";

JSDOM.fromURL("https://example.com/", options).then(dom => {
  console.log(dom.serialize());
});

JSDOM.fromFile("stuff.html", options).then(dom => {
  console.log(dom.serialize());
});

const dom = new JSDOM();
dom.window.top === dom.window;
dom.window.location.href === "about:blank";
dom.reconfigure({ windowTop: myFakeTopForTesting, url: "https://example.com/" });
dom.window.top === myFakeTopForTesting;
dom.window.location.href === "https://example.com/";


const { Script } = require("vm");
const dom = new JSDOM(``, { runScripts: "outside-only" });
const s = new Script(`
  if (!this.ran) {
    this.ran = 0;
  } 
  
  ++this.ran;
`);
dom.runVMScript(s);
dom.runVMScript(s);
dom.runVMScript(s);
dom.window.ran === 3;

const dom = new JSDOM(`<!DOCTYPE html>hello`);
dom.serialize() === "<!DOCTYPE html><html><head></head><body>hello</body></html>";
dom.window.document.documentElement.outerHTML.outerHTML === "<html><head></head><body>hello</body></html>";

const dom = new JSDOM(
  `<p>Hello
    <img src="foo.jpg">
  </p>`,
  { includeNodeLocations: true }
);

const document = dom.window.document;
const bodyEl = document.body;
const pEl = document.querySelector("p");
const textNode = pEl.firstChild;
const imgEl = document.querySelector("img");

console.log(dom.nodeLocation(bodyEl));
console.log(dome.nodeLocation(pEl));
console.log(dom.nodeLocation(textNode));
console.log(dom.nodeLocation(imgEl));
```

```
```


