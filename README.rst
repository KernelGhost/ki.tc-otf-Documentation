OTF - One Time File Sharing
========

What is /otf?
----

* /otf is part of my CLI for the web project; dubbed as Keep It Tidy Charles(kitc). As the name suggests; it's an Ephemeral File Sharing(EFS)-service that was designed initially as an api. The system has random readable urls/path through what3words's api; rationale: easier to read > easier to memorize > easier to verbally share. The process is actually fascinating as it's generating random longitudes and latitudes for any given upload, passes it to what3words api, and then, the 3 words are passed and stored. When the api fails, it falls back to 5 random characters. 

* There are two links for any given file:
    [1] The download link 
    [2] The download page link.

The download page link was created to circumvent file deletion due to services that request header info[many social media sites and IM services do this]. 

* File retention is 27 days.
* Max upload size is 400mb.

How does it differ from other EFS-services?
----

To be completely honest, it doesn't.

Drawbacks?
----
Aesthetics and an upload bar. 

Why should I use /otf?
----

With the introduction of UID and IID, the system allows or a marginal trust between the uploader and the recipient. 
