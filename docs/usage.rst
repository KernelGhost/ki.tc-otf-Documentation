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

IID stands for Issuer Identification; it’s a basic sha256 hash of the uploader's ip address and a secret salt. It signifies an ip change.

UID stands for User Identification; it acts like a regular api key for verified uploads. The resultant of which is UIDCERT, the certificate used to identify approved uploads. The certificate is the user’s email + a shared secret checksum.

The logic behind adding UID and UIDCERT is to verify that someone using Alice’s UID did in fact upload the file. Alice’s email is not accessible without the UID hash. The system relies on Alice’s complete trust in the service. Bob can easily check whether or not alice did in fact upload the file by calculating the hash of Alice’s known email and the provided secret.

	echo -n alice@crypto.com:secret | sha256sum
	
IID will act as warning later on, the system will keep track of iid’s and notify users if it’s changed.  

Verified uploads are API dependent, the web version doesn’t support UID. UID and SECRET should be passed as a header-not the best way to do it, will look into alternatives::

	curl -i -H "uid:2fc08571a5350a038b27" -H "secret:TEST" -F "file=@Screenshot_20160729_014.png" https://ki.tc/file/u/

	{
	  "file": {
	    "_id": "drogue.weddings.collectivist",
	    "approved": "USER'S EMAIL",
	    "download_page": "https://ki.tc/file/drogue.weddings.collectivist",
	    "file": [
	      "File Name: Screenshot_20160729_014.png",
	      "Content Type: image/png"
	    ],
	    "iid": "f288ca7ea7fb04229e22e33c0e819fc941c703e55ba82d0121dc3f79",
	    "length": "526K",
	    "link": "https://ki.tc/f/drogue.weddings.collectivist",
	    "sha256": "98ad20a92f29c8b0e815f266c661975cfc11375e7d92a3b55bf13f78057736cc",
	    "time": "Sun, 03 Mar 2019 11:10:14 GMT",
	    "uidcert": "b3c3e382cea7b4b6104cc268b08838bd410bc9f6cbf16e39f32f218d"
	  }
	  
If UID is passed, SECRET must be passed as well or the system will fallback to an internal server error.


