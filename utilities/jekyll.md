---
    layout: page
    title:  ""
---


### Jekyll Utilities

1. To run the PsionmanSet on  the local server:

    {%- capture code -%}
    bundle exec jekyll serve --baseurl '' --port 4200
    {%- endcapture -%}
    {% include code_snippet.md code=code language='python' %}


    {% capture code %}The quick fox{% endcapture %}

```javascript
/* Global scope: this code is executed once */
const redis = require('redis');

const host = <HOSTNAME>;
const port = <PORT>;
const password = <PASSWORD>;

...
```
{: #code-example-1}



{% if page.content contains "code" %}
<script>
<!-- clipboard.js code -->
</script>
{% endif %}


// get all <code> elements


var allCodeBlocksElements = $( "code" );

allCodeBlocksElements.each(function(i) {
 	// add different id for each code block

	// target
  var currentId = "codeblock" + (i + 1);
  $(this).attr('id', currentId);

  //trigger
  var clipButton = '<button class="btn" data-clipboard-target="#' + currentId + '"><img src="https://clipboardjs.com/assets/images/clippy.svg" width="13" alt="Copy to clipboard"></button>';
     $(this).after(clipButton);
  });

  new Clipboard('.btn');

  <script src="https://code.jquery.com/jquery-3.2.1.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/clipboard@1/dist/clipboard.min.js"></script>


<code>print("Club Nacional de Football")</code>
<br>
<code>print("is a sports institution")</code>
<br>
<code>print("from Uruguay")</code>
