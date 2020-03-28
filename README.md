## content-inject-plugin
a plugin for html-webpack-plugin，which can inject static file content into html page

## Usage
```javascript
var ContentInjectPlugin = require('./plugins/contentInjectPlugin');

new ContentInjectPlugin({
    contents:{
        content: 'this is inject content',
        rem: function(){
            return fs.readFileSync('./src/static/js/rem.js',{encoding:'utf8'});
        },
        other: 'other file content'
    },
    replaceMode: 'all',
    memo: true
})
```   
in template

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <title>template</title>
        <meta charset="utf-8">
        <meta name="hotcss" content="design-width=750">
        <meta name="apple-mobile-web-app-capable" content="yes">
        <meta content="black" name="apple-mobile-web-app-status-bar-style">
        <meta content="telephone=no" name="format-detection">
        <script>
        {{{__rem__}}}
        </script>
        <script>
        {{{__other__}}}
        </script>
    </head>
    <body>
        <div id="app">
        </div>
        {{{__other__}}}
    </body>
</html>
```

## Params

Parameter | Type | Default | Options | Description
--------- | ---- | ------| ----- |---------------
contents    | `array` |  |  | the content's array, which key used by tag in template, like `{{{__key__}}}`, support function to get content
replaceMode   | `string` | all | all,first | replace all matches or the first match
memo | `boolean` |  |  | memorize the content or not

## Note

In tempalte, content tag, which want to inject into head, must use legal tag like <script> wrapped, if not, it will be injected into body.