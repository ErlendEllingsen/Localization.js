![Localization.js Logo](https://i.imgur.com/VP9qZnR.png)

# Localization.js
Javascript platform for localization and globalization of documents, web pages, web applications et cetra. 

*Localization.js* uses JSON-documents to store translations. A typical file structure of an app using *Localization.js* would be:

```
 locale/ 
 	config.json
 	en-us/
 		login.json
 	no-nb/
 		login.json
 app.js
```

##Install
###NPM
***Note:*** *This is not a node-package, but recommended installation is still through npm.*

`npm install localization-js --save`

###Zip
[Download latest release](https://github.com/ErlendEllingsen/Localization.js/releases).

##Usage 
*localization.js* is rather lightweight and easy to setup.

1. Create a new instance `var lang = new Localization();`
2. Initialize the instance `Localization.initialize(config_path, completedCallback);`
3. Set locale `lang.setLocale(language);`
4. Load modules `lang.loadModule(module_filename, callback);`
5. Start processing text `lang.processContent(data, variableArray);`

*For more, please see the example of usage (below).* 

###Example of usage 
The following example is from one of my hybrid web apps. 

**app.js**

```javascript
var lang = new Localization();
lang.initialize('locale/config.json', function(){
    //Initialized     
    lang.setLocale('no-nb'); //e.g. "en-us"
    
    lang.loadModule('login.json', function(){
        //Loaded
	
		//Fetch some data over ajax	
		$.get('./login.html', function(data){
		
			//Convert content to language
			data = lang.processContent(data, [
			    'login_title',
			    'login_email_placeholder',
			    'login_password_placeholder',
			    'login_button_text',
			    'login_not_a_member_text',
			    'login_sign_up'
			]);
			
			$('#pre-login').html(data);
			login.bindings();
		});
	 
	 	//end lang.loadModule		
    });
    //end lang.initialize
});
```

**./locale/config.json** (*localization.js* configuration file)

```JSON
{
    "supported_locales": ["no-nb", "en-us"]
}
```

**./locale/en-us/login.json** (English American language file)

```JSON
{
    "title": "login",
    "content": {
        "login_title": "Login",
        "login_email_placeholder": "E-mail",
        "login_password_placeholder": "Password",
        "login_button_text": "Login",
        "login_not_a_member_text": "Not a member?",
        "login_sign_up": "Sign up"
    }
}
```

**./locale/no-nb/login.json** (Norwegian language file)

```JSON
{
    "title": "login",
    "content": {
        "login_title": "Innlogging",
        "login_email_placeholder": "E-post",
        "login_password_placeholder": "Passord",
        "login_button_text": "Logg inn",
        "login_not_a_member_text": "Ikke medlem?",
        "login_sign_up": "Opprett bruker"
    }
}
```


##License
MIT License

Copyright (c) 2016 Erlend Ellingsen

See `LICENSE`-file.
