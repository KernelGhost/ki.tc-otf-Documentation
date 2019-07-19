========
Usage
========
	
>_CLI::

	curl -F "file=@59b5b" https://ki.tc/file/u/
 {
  "file": {
    "_id": "perfecting.classics.postsurgical",
    "approved": "False",
    "download_page": "https://ki.tc/file/perfecting.classics.postsurgical",
    "file": [
      "File Name: 59b5b",
      "Content Type: application/octet-stream"
    ],
    "ip256": "2d54e0e74f8881713a7ea858fcdbe18f02d132ba640028f6b1c6a7b2a8d18446",
    "length": "3K",
    "link": "https://ki.tc/f/perfecting.classics.postsurgical",
    "sha256": "d81dd207b277be80af3698b0872da2a35ae733f19c07b17b2cc41ca8ae1cf39a",
    "time": "Fri, 19 Jul 2019 20:20:10 GMT"
  }
 }

Random readable urls/path; rationale: easier to read > easier to memorize > easier to verbally share. When the w3w api fails, it falls back to 5 characters::

	curl -F "file=@59b5b" https://ki.tc/file/u/
  {
  "file": {
    "_id": "4fed2",
    "approved": "False",
    "download_page": "https://ki.tc/file/4fed2",
    "file": [
      "File Name: 59b5b",
      "Content Type: application/octet-stream"
    ],
    "ip256": "2d54e0e74f8881713a7ea858fcdbe18f02d132ba640028f6b1c6a7b2a8d18446",
    "length": "3K",
    "link": "https://ki.tc/f/4fed2",
    "sha256": "d81dd207b277be80af3698b0872da2a35ae733f19c07b17b2cc41ca8ae1cf39a",
    "time": "Fri, 19 Jul 2019 20:20:10 GMT"
  }
 }

.. image:: https://i.imgur.com/Pwu98HJ.gif
	
DONT TRUST THE SERVICE....ALWAYS ENCRYPT::

	keybase encrypt -i Raspberry_Pi_Logo.svg.png -o r_keybase chris

	openssl enc -aes-256-cbc -salt -in Raspberry_Pi_Logo.svg.png -out r_encrypted
	
	

**Using IID and UID:**


Generate UID::

  curl -X POST -F 'keybase_id=YOUR_KEYBASE-USERNAME' https://ki.tc/otf/generate_key

    {
    "generate_key": {
        "Attention": "Make sure it's public",
        "Instructions": "Create a text file under /otf so that --> https://keybase.pub/YOUR_KEYBASE-USERNAME'/otf/otf_key.txt Use /check_key to validate your uid",
        "keybase_id_status": true,
        "uid": "9ff40341dc7c978839abd831595f65ef2b4aba9cda79d7c1057f335ac6dd66ec"
    }    

.. image:: https://i.imgur.com/ryqqS4r.gif
.. image:: https://i.imgur.com/jwhVf5m.gif
	  
Check UID in Keybase, make sure you have created https://keybase.pub/YOUR_KEYBASE-USERNAME/otf/otf_key.txt::



	curl -X POST -F 'uid=9ff40341dc7c978839abd831595f65ef2b4aba9cda79d7c1057f335ac6dd66ec' https://ki.tc/otf/check_key

	{
	  "check": {
	    "Attention": "Do not lose your iid",
	    "iid": "ca98cc2b5cd7d1b8cabaa748a252623c54c65942a608b315bfe2dcfb44cd66e7",
	    "match_condition": true
	  }
	  
.. image:: https://i.imgur.com/V6xAvEi.gif

Upload using your new IID::

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

.. image:: https://i.imgur.com/9OerKar.gif

.. image:: https://i.imgur.com/FxE42Rn.gif



 
