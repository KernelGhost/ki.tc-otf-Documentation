========
Usage
========
	
>_CLI::

	curl -F 'file=@Screenshot_20160729_014.png' http://ki.tc/file/u/
	{
	  "file": {
	    "_id": "downsizing.revolved.fervently",
	    "approved": "False",
	    "download_page": "https://ki.tc/file/downsizing.revolved.fervently", 
	    "file": [
	      "File Name: Screenshot_20160729_014.png", 
	      "Content Type: image/png", 
	      "length: 526K"
	    ], 
	    "iid": "f288ca7ea7fb04229e22e33c0e819fc941c703e55ba82d0121dc3f79",
	    "link": "https://ki.tc/f/downsizing.revolved.fervently", 
	    "sha256": "98ad20a92f29c8b0e815f266c661975cfc11375e7d92a3b55bf13f78057736cc", 
	    "time": "Tue, 12 Dec 2017 01:48:13 GMT"
	  }
	}
	
Random readable urls/path; rationale: easier to read > easier to memorize > easier to verbally share. When the w3w api fails, it falls back to 5 characters::

	curl -F 'file=@Screenshot_20160729_014.png' http://ki.tc/file/u/
	{
	  "file": {
	    "_id": "4fde2", 
	    "download_page": "https://ki.tc/file/4fde2", 
	    "file": [
	      "File Name: Screenshot_20160729_014.png", 
	      "Content Type: image/png"
	    ], 
	    "length": "526K", 
	    "link": "https://ki.tc/f/4fde2", 
	    "sha256": "98ad20a92f29c8b0e815f266c661975cfc11375e7d92a3b55bf13f78057736cc", 
	    "time": "Tue, 12 Dec 2017 01:53:01 GMT"
	  }
	}
	
DONT TRUST THE SERVICE....ALWAYS ENCRYPT::

	keybase encrypt -i Raspberry_Pi_Logo.svg.png -o r_keybase chris

	openssl enc -aes-256-cbc -salt -in Raspberry_Pi_Logo.svg.png -out r_encrypted
	
	
====
Understanding IID and UID
====
Generate UID:

	curl -X POST -F 'keybase_id=YOUR_KEYBASE-USERNAME' https://ki.tc/otf/generate_key


	{
	  "generate_key": {
	    "Attention": "Make sure it's public",
	    "Instructions": "Create a text file under /otf so that --> https://keybase.pub/YOUR_KEYBASE-USERNAME'/otf/otf_key.txt Use /check_key to validate your uid",
	    "keybase_id_status": true,
	    "uid": "9ff40341dc7c978839abd831595f65ef2b4aba9cda79d7c1057f335ac6dd66ec"
	  }

	  
Check UID in Keybase, make sure you have created https://keybase.pub/YOUR_KEYBASE-USERNAME/otf/otf_key.txt

	curl -X POST -F 'uid=9ff40341dc7c978839abd831595f65ef2b4aba9cda79d7c1057f335ac6dd66ec' https://ki.tc/otf/check_key

	{
	  "check": {
	    "Attention": "Do not lose your iid",
	    "iid": "ca98cc2b5cd7d1b8cabaa748a252623c54c65942a608b315bfe2dcfb44cd66e7",
	    "match_condition": true
	  }
	  
Upload using your new IID

	curl i -H "iid:ca98cc2b5cd7d1b8cabaa748a252623c54c65942a608b315bfe2dcfb44cd66e7"  -F "file=@59b5b" https://ki.tc/file/u/
	
	
	HTTP/1.1 100 Continue

	HTTP/1.1 201 CREATED
	Date: Fri, 19 Jul 2019 19:02:28 GMT
	Server: Apache/2.4.18 (Ubuntu)
	Content-Length: 635
	Content-Type: application/json

	{
	  "file": {
	    "_id": "carnality.elderly.unreservedly",
	    "approved": "YOUR_KEYBASE-USERNAME@ki.tc",
	    "download_page": "https://ki.tc/file/carnality.elderly.unreservedly",
	    "file": [
	      "File Name: 59b5b",
	      "Content Type: application/octet-stream"
	    ],
	    "ip256": "79f4fe7c35ed5cba2b5c74613e017a84680d7f96848303038de418b1fc23f71a",
	    "length": "3K",
	    "link": "https://ki.tc/f/carnality.elderly.unreservedly",
	    "sha256": "d81dd207b277be80af3698b0872da2a35ae733f19c07b17b2cc41ca8ae1cf39a",
	    "time": "Fri, 19 Jul 2019 19:02:28 GMT",
	    "uidcert": "544a9894a7033d2dc8a1f822f7d9e78ed2baa56bfabffa9c5efc96a226180cb6"
	  }

![Keybase Tag]
(https://i.imgur.com/rnYwV3p.png)

Note the Keybase tag


