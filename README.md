REPO IS NOT MAINTANED - ARCHIVING AS READ ONLY

Install everything:

```
 $ npm install
```

Build the Javascript bundle

```
 $ npx webpack
```

Now you can open `dist/index.html` in the browser.

Or you can run it from the command

```
 $ npm start
```

## TESTING

In the main script the following constants can be found:

```
const AUTHORUSER = "beefc6472de3bba1d389ad8b18348c3df50d680c"; 
const SCRIPTFEEDTOPIC = "646973706f636861745f73637269707400000000000000000000000000000000"; // name = dispochat_script
const SCRIPTFEEDHASH = "c8b0051d921ae84f1676a24eaa7d509302dfbd9902dea17fbebe9e004a4a119b"; 
const HTMLFEEDTOPIC = "646973706f636861745f68746d6c000000000000000000000000000000000000"; // name = dispochat_main, topic 
const HTMLFEEDHASH = "4dce80c0210b318db31094a1e7c694179b24ac22b56f25d44582800f0ca07706";
```

To test the automatic responder script generation and upload logic works correctly, update the `SCRIPTFEEDTOPIC` and `HTMLFEEDTOPIC` feeds with _manifests_ enclosing the following data:

**HTMLFEEDTOPIC (index.html):**

```
<html>
<head>
<script language="javascript" src="head.js"></script>
<script language="javascript" src="main.js"></script>
</head>
<body>
loaded...
</body>
</html>
```

**SCRIPTFEEDTOPIC (main.js):**

```
console.log(keyTmpRequestPriv);
```

Replace the `HTMLFEEDHASH` and `SCRIPTFEEDHASH` constants with the corresponding resulting hashes. Also nodify the `AUTHORUSER` with the user used to update the feeds.

Then run the script and look for `published manifest: <HASH>` in the output.

---

To test the connection logic:

1. run ts-node ./src/index.ts in terminal 1, and while running...
1. look for `tmp priv: <HASH>` in the output, and copy the hash
1. run ts-node ./src/index.ts <HASH> in terminal 2
