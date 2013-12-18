# wut

A small Javascript templating library.

Don't write Javascript in your templates, write your templates in Javascript.

Usage:

```javascript
var wut = require('wut');
var makeTag = wut.makeTag;

// Create some tags:
var html = makeTag("html");
var body = makeTag("body");
var ul = makeTag("ul");
var li = makeTag("li");
var p = makeTag("p");
var a = makeTag("a");

// Or pollute the scope with HTML5 premade tag functions:
wut.pollute(this);

// Use a single tag:
p("foo"); 
//=> <p>foo</p>

// Use a self-closing tag by omitting the innerHTML:
hr();
//=> <hr/>

input({value: "mytest"});
//=> <input value="mytest"/>

// Empty string for empty tag:
p("");
//=> <p></p>

// Nest some tags:
doctype("html") +
html(
  body(
    ul(
      li("Item one"),
      li("Item two")
    ),
    hr()
  )
);
//=> <html><body><ul><li>Item one</li><li>Item two</li></ul><hr/></body></html> 

// Set attributes:
a({href: "http://google.com"}, "Click Here");
// => <a href='http://google.com'>Click Here</a>

// Output a script tag with real javascript:
script({type: "text/javascript"}, 
  function() {
    var i = 10;
    i += 1;
  }
);

/* Outputs:
<script type="text/javascript">
  function() {
    var i = 10;
    i += 1;
  }();
</script>
*/

var html = makeTag("html");
var body = makeTag("body");
var p = makeTag("p");
var span = makeTag("span");
var head = makeTag("head");
var script = makeTag("script");
var div = makeTag("div");
var input = makeTag("input");
var hr = makeTag("hr");

// Angular.js app (it actually works!):
doctype("html") +
html({"ng-app":null},
  head(
    script({src:"http://code.angularjs.org/1.2.5/angular.min.js"}),
    script(function() {
      function HelloCntl($scope) {
        $scope.name = 'World'l
      }
    })
  ),
  body(
    div({"ng-controller":"HelloCntl"},
      span(
        p("Your Name: "),
        input({type:"text", "ng-model":"name"}),
        hr(),
        p("Hello {{name || 'world'}}!")
      )
    )
  )
);
```

## Installation

`npm install wut`

### License

(c) 2013 Alan deLevie. See `package.json` for license.
