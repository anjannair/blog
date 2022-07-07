---
title: Split Large HTML Files
description: Learn how to split large HTML files into smaller files statically, without any extra installations.
image_url: https://www.udacity.com/blog/wp-content/uploads/2020/06/HTML_Blog-scaled.jpeg
---

# Splitting Big HTML Files
React and many other frameworks have the ability to split big chunks of code into different files to make the work of the programmer easier. What if I tell you the same can be done for HTML static sites too?

## Getting Into It
Mind you, I am not the author of this code but just for the sake of documenting everything new I find, I am writing this down. This code has been picked up from a StackOverflow thread (I do not have the link of the original thread but if I do come across it again I will make sure to link it)

**The code -**
```js
function HTMLImporter() {}

HTMLImporter.import = function (url) {
  var error, http_request, load, script;

  script =
    document.currentScript || document.scripts[document.scripts.length - 1];

  load = function (event) {
    var attribute, index, index1, new_script, old_script, scripts, wrapper;

    wrapper = document.createElement("div");
    wrapper.innerHTML = this.responseText;

    scripts = wrapper.getElementsByTagName("SCRIPT");

    for (index = scripts.length - 1; index > -1; --index) {
      old_script = scripts[index];

      new_script = document.createElement("script");
      new_script.innerHTML = old_script.innerHTML;

      for (index1 = old_script.attributes.length - 1; index1 > -1; --index1) {
        attribute = old_script.attributes[index1];
        new_script.setAttribute(attribute.name, attribute.value);
      }

      old_script.parentNode.replaceChild(new_script, old_script);
    }

    while (wrapper.firstChild) {
      script.parentNode.insertBefore(
        wrapper.removeChild(wrapper.firstChild),
        script
      );
    }

    script.parentNode.removeChild(script);

    this.removeEventListener("error", error);
    this.removeEventListener("load", load);
  };

  error = function (event) {
    this.removeEventListener("error", error);
    this.removeEventListener("load", load);

    alert("there was an error!");
  };

  http_request = new XMLHttpRequest();
  http_request.addEventListener("error", error);
  http_request.addEventListener("load", load);
  http_request.open("GET", url);
  http_request.send();
};
```

## How to use it
Import the code into your main HTML file by adding the whole JS code into a file and using the script tag to do so. 

**Important** - Add the import script at the top before you import your components

After importing the importer code use the following to easily integrate the component into your file -

```js
<script>HTMLImporter.import("./path/to/file")</script>
```

That is it!! You can now split your HTML file into multiple files and yes this works for static websites too!
