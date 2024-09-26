######################################
`ki.tc/otf <https://ki.tc/otf>`_ Usage
######################################

++++++++++++++++++++++++++++
Command Line Interface (CLI)
++++++++++++++++++++++++++++

To upload a file named ``File Name.ext``, first navigate to the directory containing the file and then enter the following command in your shell::

  curl -X POST -F "file=@File Name.ext" https://ki.tc/file/u/

A successful upload will return a JSON response structured as follows::

  {
    "file": {
      "_id": "perfecting.classics.postsurgical",
      "approved": "False",
      "download_page": "https://ki.tc/file/perfecting.classics.postsurgical",
      "file": [
        "File Name: File Name.ext",
        "Content Type: application/octet-stream"
      ],
      "ip256": "2d54e0e74f8881713a7ea858fcdbe18f02d132ba640028f6b1c6a7b2a8d18446",
      "length": "3K",
      "link": "https://ki.tc/f/perfecting.classics.postsurgical",
      "sha256": "d81dd207b277be80af3698b0872da2a35ae733f19c07b17b2cc41ca8ae1cf39a",
      "time": "Fri, 19 Jul 2019 20:20:10 GMT"
    }
  }

In the above example, the download page link is https://ki.tc/file/perfecting.classics.postsurgical.

Creating random readable URLs using words from the English dictionary is beneficial for several reasons:

#. They are easier to read.
#. They are simpler to memorize.
#. They are more convenient for verbal sharing.

In cases where the `what3words API <https://developer.what3words.com/public-api>`_ fails, the system will default to a 5-character identifier. For example::

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

In the above example, the download page link is https://ki.tc/file/4fed2.

++++++++++
Encryption
++++++++++

**Do not trust the OTF service - ALWAYS encrypt sensitive files!**

To encrypt a file using `Keybase <https://keybase.io/>`_ such that only 'chris' can decrypt the file, run::

  keybase encrypt -i Raspberry_Pi_Logo.svg -o encrypted_file chris

To encrypt a file using OpenSSL with AES-256-CBC, run::

  openssl enc -pbkdf2 -aes-256-cbc -salt -in Raspberry_Pi_Logo.svg -out encrypted_file
  
OpenSSL will prompt you to enter a passphrase in order to encrypt the file.

+++++++++++++++++++
Using IIDs and UIDs
+++++++++++++++++++
* UIDs (User IDs): Uniquely identify users.
* IIDs (Instance IDs): Uniquely identify specific instances of objects or resources.

To generate a UID using your `Keybase <https://keybase.io/>`_ username, execute the following command::

  curl -X POST -F 'keybase_id=YOUR_KEYBASE-USERNAME' https://ki.tc/otf/generate_key

A successful request will return a JSON response structured as follows::

  {
    "generate_key": {
      "Attention": "Make sure it's public",
      "Instructions": "Create a text file under /otf so that --> https://keybase.pub/YOUR_KEYBASE-USERNAME'/otf/otf_key.txt Use /check_key to validate your uid",
      "keybase_id_status": true,
      "uid": "9ff40341dc7c978839abd831595f65ef2b4aba9cda79d7c1057f335ac6dd66ec"
    }
  }

In the above example, the UID is ``9ff40341dc7c978839abd831595f65ef2b4aba9cda79d7c1057f335ac6dd66ec``.

.. image:: https://i.imgur.com/ryqqS4r.gif

Once your UID has been created, ensure it is stored at https://keybase.pub/YOUR_KEYBASE-USERNAME/otf/otf_key.txt.

.. image:: https://i.imgur.com/jwhVf5m.gif

To check your UID, run::

  curl -X POST -F 'uid=9ff40341dc7c978839abd831595f65ef2b4aba9cda79d7c1057f335ac6dd66ec' https://ki.tc/otf/check_key

A successful request will return a JSON response containing an IID::

  {
    "check": {
      "Attention": "Do not lose your iid",
      "iid": "ca98cc2b5cd7d1b8cabaa748a252623c54c65942a608b315bfe2dcfb44cd66e7",
      "match_condition": true
    }
  }

In the above example, the returned IID is ``ca98cc2b5cd7d1b8cabaa748a252623c54c65942a608b315bfe2dcfb44cd66e7``.

.. image:: https://i.imgur.com/V6xAvEi.gif

Finally, you can upload a file (e.g. ``Example File.ext``) using the IID issued above::

  curl i -H "iid:ca98cc2b5cd7d1b8cabaa748a252623c54c65942a608b315bfe2dcfb44cd66e7" -F "file=@Example File.ext" https://ki.tc/file/u/

A successful request will return a JSON response structured as follows::

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

In the above example, the download page link is https://ki.tc/file/carnality.elderly.unreservedly.

.. image:: https://i.imgur.com/9OerKar.gif

The recipient can verify your UID on the download page to confirm your identity as the sender.

.. image:: https://i.imgur.com/FxE42Rn.gif
