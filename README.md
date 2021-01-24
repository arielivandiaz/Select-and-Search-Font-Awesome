## Select and Search engine for FontAwesome

Visit the demo of this project:
[![DEMO](https://raw.githubusercontent.com/arielivandiaz/Select-and-Search-Font-Awesome/master/readme/demoGIF.gif)](https://github.com/arielivandiaz/lagunite)






### Generate the icon list from FontAwesome files

Inside the *"generate.html"* file the script reads the fontawesome stylesheet and collects all the classes that correspond to each icon.

```js
fetch("brands.json")
            .then(response => response.json())
            .then(brands => {
                var panel = document.getElementById("icons");
                var started = 0;
                var firstItem = "fa-500px";
                var lastItem = "fa-zhihu";
                Array.prototype.forEach.call(document.styleSheets[0].cssRules, function(a) {
                    var di = document.createElement("i");
                    var icon = a.selectorText;
                    if (icon != undefined)
                        icon = icon.replace(".", "").replace("::before", "");
                    if (started == 0)
                        if (icon === firstItem) started = 1;
                    if (started == 1) {
                        di.dataset.lagunite = icon.replace(/-/g, ' ').slice(3);
                        if (brands[icon])
                            di.classList.add("fab");
                        else
                            di.classList.add("fas");
                        di.classList.add(icon);
                        di.onclick = function(event) {
                            console.log(icon);
                            navigator.clipboard.writeText(icon);
                        }
                        panel.appendChild(di);
                        if (icon === lastItem)
                            started = 0;
                    }
                })
            });
```

To filter only the icons define the variables *firstItem* and *lastItem*.

The regular icons use the class *"fas"* and the brand icons use the class *"fab"* to check this the script consults the file brands.json that contains the definitions of the icons that are brands. If you use FontAwesome premium or other versions you can edit this procedure accordingly.

The custom lagunite attribute is used later to use the icon search engine.




The project is made using Lagunite.


[![Lagunite](https://raw.githubusercontent.com/arielivandiaz/Select-and-Search-Font-Awesome/master/lagunite/lagunite.png)](https://github.com/arielivandiaz/lagunite)




