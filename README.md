# Gerrit File Watcher
Watches files on Gerrit and adds a reviewer and an optional message.

# How to use
Make sure you have the Paramiko, Cheetah and [Python Gerrit Bindings](https://github.com/ficoos/python-gerrit) installed.

Create a configuration file under `$HOME/.config/gerrit-file-watcher/conf.json'

An example configuration file:

```json
{
        // optional, uses ~/.ssh/id_rsa by default
        "key_file": "path/to/private/key.rsa",
	// optional, will use current username by defaul
	"username": "user_name",
	// port is optional
	"address": "gerrit.example.com:29418",
	// filters are python regular exceptions
	"filters" : {"project_name": [
		"^doc/",
		"^folder/specific_file$",
		"^folder/(file1|file2).ext$",
		"Makfile.am" //any Makefile.am in the project
		]}
}
```

If you want a message to be posted when adding a review you need to create a file called
`$HOME/.config/gerrit-file-watcher/template.tmpl'

This is a Cheetah template which gets the following variables:
* username
* files
* project

Example template:
```cheetah
One of $username's automated scripts discovered this patch might require his approval.
Please wait until he had time to check it out.

```
