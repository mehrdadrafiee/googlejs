GoogleJS
======
Google APIs made easy

###Getting Started###
```html
<script src="main.js"></script>
<script type="text/javascript" src="https://apis.google.com/js/client.js?onload=loadDrive"></script>
<script src="googlejs.js"></script>
```

You also need to get some information from the Google Developer Console. You will be able to access this information [here](https://console.developers.google.com/project).

You need:
+ the client id
+ the app id
+ the developer key

You also need to add the Google Drive API and Google Drive SDK through the developer console, and to set the javascript origin and redirect urls based on the url you want to use **googlejs** from. For more information, go [here](https://developers.google.com/drive/web/enable-sdk). 

For example,

```javascript
function loadDrive(){
	//this function is called once the API is loaded
	
	googlejs.clientId = '953350323460-0i28dhkj1hljs8m9ggvm3fbiv79cude6.apps.googleusercontent.com';
	googlejs.appId = '953350323460';
	googlejs.developerKey = 'AIzaSyBTSFIgQkLly9v6Xuqc2Nqm-vX0jpyEbZk';
}
```

###Things to Know###
Each Google Drive file, folder, and user has a unique id. You can find the id of a file or folder by using the `pickFile()` or `pickerFolder()` methods. These will return an object, which can be parsed for the id.

Each user also has a root folder (the highest level folder in your Google Drive file tree). This is stored under `googlejs.rootFolderId` once the `googlejs.loadDrive()` method is called and executed.

###Checking Login Status###
One thing that you might want to do is to check if the user is already logged in.

```javascript
function loadDrive(){
	googlejs.clientId = '953350323460-0i28dhkj1hljs8m9ggvm3fbiv79cude6.apps.googleusercontent.com';
	googlejs.appId = '953350323460';
	googlejs.developerKey = 'AIzaSyBTSFIgQkLly9v6Xuqc2Nqm-vX0jpyEbZk';
	
	googlejs.isLoggedIn(function(res,err){
		if(res === true){
			//already logged in
		} else {
			//not yet logged in, need to be authorized
		}
	});
}
```

###Logging User In###
There are two ways to log the user in. One is to redirect the user to a specific url, which then redirects the user again, once the authorization is complete to another (`redirect_url`). This url must be specified in the Google Developer console's "credidentials" section.

```javascript
googlejs.login(true, function(){
	//the user will be redirected via window.location.href
},"https://example/blahblahblah");
```

The other way creates a popup that authorizes the user.

```javascript
googlejs.login(false, function(){
	
},"");
```

###Loading Drive###
```javascript
googlejs.loadDrive(function(){
	
});
```

###Getting User Info###
<b>Before you can get user information, you must load Google Drive (see above)</b>

Knowing information such as the email and storage space of a user is important. The `googlejs.getInfo()` method will return this information as an object.

```javascript
googlejs.getInfo(function(res){
	console.log(res);
});
```

**Todo**
+ token refresh (done)
+ Google Drive
  + log in (done)
  + log out (done)
  + check if logged in (done)
  + open file dialog (done)
  	+ file (done)
  	+ folder (done)
  + upload dialog (done)
  + share dialog (done)
  + get contents (done)
  + make changes (done)
  + get title (done)
  + rename (done)
  + get file metadata (done)
  + new file (done)
  + add file to folder (done)
  + remove file from folder (done)
  + get stuff
  	+ parents  (done)
  	+ all files (done)
  	+ files in folder (done)
+ Google Realtime
  + detect changes
  + make changes
  + get collaborators
+ info
  + get user info (done)
