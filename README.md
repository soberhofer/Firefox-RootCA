# Firefox-RootCA
## Adding RootCA to Firefox 

 Since Firefox does not look for trusted Certificates in the User's or the System's Keychains, they have to be manually added into the .app

 This is fairly straightforward but there are a few steps which are quite tricky.

### 1.) Download `mozilla.cfg` and `local-settings.js` 

### 2.) Edit the `mozilla.cfg` 
Insert the base64 encoded certificate WITHOUT any line breaks and without the 
`------BEGIN CERTIFICATE------` 
and 
`------END CERTIFICATE------` bits. 

The Certificate should be put in a variable with `certname = "CERTGOESHERE";`

To load the Certificate, the line `certdb.addCertFromBase64(certname, "C,C,C", "");` is needed afterwards. 

There can be an arbitrary Number of Certificates in the file.

Please note that the first line of the file (for whatever reason) NEEDS to be a comment.

### 3.) move the files

`mv ./mozilla.cfg /Applications/Firefox.app/Contents/Resources/mozilla.cfg` 

`mv ./local.settings.js /Applications/Firefox.app/Contents/Resources/defaults/pref/local-settings.js`

This needs to be done as root and can be done manually or via a Firefox postinstall or outset boot script.

### 4.) Restart Firefox. From now on your root CA should be trusted.
