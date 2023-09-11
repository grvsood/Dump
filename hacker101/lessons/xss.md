## XSS
1. Reflected xss - input from user goes directly to browser and thus permissitng injection of content
2. stored xss - input gets stored on server and returned layer everytime user access that database 
3. DOM xss - input is injected into DOM without proper escaping. 


Recognition -
1. find where data goes. is it in a tag attribute or can it be embedded to script tag?
2. find special handling.  does urls get turned into links? 
3. check special characters: '<>:;"


- try dom events like on mouse hover 
- <script>alert(1)</script>  or try anchor tag or image tag or work around with on error attribute.. if somethings is detecting script tag.
- when inputs change to links we can send in code for example `<a  href="https://"onmouseover="alert(1);">` when victim hovers over they have it in action. this syntax is same as writting valid html `<a href="https://somelink"style="..">` 
- for example <script> var token = 'user input here'; </script> is vulenrable. exploit by using HTML entity enco ding - enter the payload ';alert(1);' and then  <script> var token = ''; alert(1);''; </script> . thus exploited. 
even better you can now even submit JS string escaped payload directly  for example enter `</script><script>alert(1);</script>` i.e final outcome is <script> var token = '</script><script>alert(1);</script> 


mitigation: 
1. escaping. has to be diffrent for each input. self doing it proabbky a failure.
2. user input shall never be part of script tag. or isnide attribute for DOM event. likelihood of mitigation is nil otherwise  


#### DOM XSS 
has to prevented client side (browser side) 100% 
mechanics are same. can happen in infinite number of eays in modern web. no off the shelf way to completely mitigate it. just dont put user inputs into pages directly. use innerText over innerHTML when putting content on the page. consider strict whitelist for these cases. 

other examples- 
* "><h1>test</h1>"
* '+alert(1)+'
* "onmouseover="alert(1)
* http://"onmouseover="alert(1)

