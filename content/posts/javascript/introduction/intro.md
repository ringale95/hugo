+++
date = '2025-02-16T06:59:55-05:00'
draft = true
title = 'Javascript'
+++
## What is Javascript?

Javascript was initially creating to make webpages alive. Program in this language is called `scripts`.

It does not require any compilation to run. JS runs directly in the browser as plain text. Browser interprets JS code line by line and executes it. Today, Javascript executes on Browser and servers or any device which has `Javascript Engine`

Different browser engines have different codenames:
- Chrome : V8
- Firefox : Spidermonkey
- Safari : SquirrelFish
- ID: Chakra

How do engines work?
- The engine reads/parse the scripts
- Converts/compiles the script to machine code
- Machine code runs fast

### Environment based Javascript:
 - In Browser
 - Node JS

**In Browser JS can do the following:** 
 - Add new content to HTML page, change existing content, modify styles
 - React to user's action, run on mouse click, pointer movements, key presses
 - Send request over network to servers `(AJAX requests)`
 - Get and set cookies
 - Store data on client side in `Local Storage`

**In Browser JS cannot do the following**:
- Does not read any arbitrary file on hard disk, copy them or execute programs. No access to OS
- Modern browser has access to files but only if user drops in browser window or select via <input> tag
- They require user's explicit permission to enable web camera and work with it
- Different tabs or windows don't know each other unless they are opened via JS events. But if they come from different website/domain/protocol still different window or tab are unaware of each other. This is `Same Origin Policy` . 
- A page from http://anysite.com should not access another browser tab with url http://gmail.com. But it can easily communicate to web server but not other sites.
- This limitation does not exists if JS is run outside browser for example on server. Modern browsers allow plugins/extensions to ask for extended permissions
