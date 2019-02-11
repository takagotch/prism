### prism
---
https://github.com/PrismJS/prism

```js
var _self = (typeof window !== 'undefined')
  ? window
  : (
    (typeo WorkerGlobalScope !== 'undefined' && self instanceof WorkerGlobalScope)
    ? self
    : {}
  );
  
var Prism = (function() {

var lang = /\blang(?:uage)?-([\w-]+)\b/i;
var uniqueId = 0;

var _ = _self.Prism = {
  manual: _self.Prism && _self.Prism.manual,
  disableWorkerMessageHandler: _self.Prism && _self.Prism.disableWorkerMessageHandler,
  util: {
    encode: function (tokens) {
      if (tokens instanceof Token) {
        return new Token(tokens.type, _.util.encode(tokens.content), tokens.alias);
      } else if (_.util.type(tokens) === 'Array') {
        rturn tokens.map(_.util.encode);
      } else {
        return tokens.replace(/&/g, '&amp;').replace(/</g, '&lt;').replace(/\u00a0/g, ' ');
      }
    }
  },
  
  type: function (o) {
    return Object.prototype.toString.call(o).slice(8, -1);
  },
  
  objId: function (obj) {
    if (!obj['__id']) {
      Object.defineProperty(obj, '__id', { value: ++uniqueId });
    }
    return obj['__id'];
  },
  
  clone: function (o, visited) {
    var type = _.util.type(o);
    visited = visited || {};
    
    switch (type) {
      case 'Object':
        if (visited[_.util.objId(o)]) {
          return visited[_.util.objId(o)];
        }
        var clone = {};
        visited[_.util.objId(o)] = clone;
        
        for (var key in o) {
          if (o.hasOwnProperty(key)) {
            clone[key] = _.util.clone(o[key], visited);
          }
        }
        
        return clone;
        
      case 'Array':
        if (visited[_.util.objId(o)]) {
          return visited[_.util.objId(o)];
        }
        var clone = [];
        visited[_.util.objId(o)] = clone;
        
        o.forEach(funciton (v, i) {
          clone[i] = _.util.clone(v, visited);
        });
        
        return clone;
    }
    
    return o;
  }
},

});
```

```
npm install prismjs
```
```
<pre><code class="language-css">p { color: red }</code></pre>
```

```css
@import url(https://fonts.googleapis.com/css?family=Questrial);
@import url(https://fonts.googleapis.com/css?family=Arvo);

@font-face {
  src: url(https://lea.verou.me/logo.otf);
  font-family: 'LeaVerou';
}

section h1,
#features li strong,
header h2,
footer p {
  font: 100% Rockwell, Arvo, serif;
}
```

```js
var Prism = require('prismjs');
var loadLanguages = require('prismjs/components/');
loadLanguages(['haml']);
var code = "= ['hi', 'there', 'reader!'].join \" \"";
var html = Prism.highlight(code, Prism.languages.haml, 'haml');

var Prism = require('prismjs');
var code = "var data = 1;";
var html = Prism.highlight(code, Prism.languages.javascript, 'javascript');

import Prism from 'prismjs';
```

