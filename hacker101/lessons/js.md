exploring vulnerabilities using JS 

- filter the network tab for JS files loading.
- open the file in sources panel yo view JS
- XHR - XML HTTP Request - fetching remote files with JS 
- can check our initiator, the line of code which initiated it 
- can search for the API resource in the panel to find the JS File associated with itz
- static analysis of JS code

####  Global listeners
shows the lists of all DOM listeners asscoaiated with the page
- check the associated file with with JS 
- in console, run the method `window.postMessage` first arg any string and second * it then runs it across all files, apply break point on JS file before running it, it will open the debugger to parse the JS 
- JS func can have diff names in diff files 
- in console, one can run the code

#### Impact
JS is protected using CORS


### examples
- iframe set it in html
- write JS to exploit it. 

```html
<body>
<iframe id=target></iframe>
...
</body>
```

```js
var target = document.getElementById('target')


target.addEventListener('load',()={
  
  target.contentWindow.postMessage("message", *)

})

target.src = "url of the page" 
```

one can write code on replit.com and share with others as POC for vulnerability found.



first thing - make it do what its suppose to do and then look for vulnerabilities.



