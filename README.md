## Drop2PI ##

First, sorry for bad English.

This is a very simple tool to sync files between Dropbox and Raspberry PI. In fact this command tools can used any system running on Python.

But I only wants to sync files to Raspberry PI. So I called this Dropbox to PI.

## What's New ##

1. download the file and folder auto.
2. modify the folder, auto sync to Dropbox.
3. delete the file or folder which deleted in Dropbox server auto.

## Need to do ##

1. config the max donload file size.
2. if there is syncing event, quit update event. (see known bug)

## Packages ##

You have to install [Watchdog](https://github.com/gorakhargosh/watchdog) first.

And also download Dropbox python SDK [HERE](https://www.dropbox.com/developers/core/sdk).

## Setup ##

#### config file ####

    cp config.py.tmp config.py

#### edit config ####

open config file and you can see code below:

	APP_KEY     = 'xj0so6fatvhx4xb'
	APP_SECRET  = 'zlwh6p1xvp9f5lk'
	ACCESS_TYPE = 'app_folder'
	TOKEN_FILE  = 'dropbox_token.txt'
	PATH_TO_WATCH = '/Users/guojing/.dropbox-sync'

You have to go to [Dropbox Develop Page](https://www.dropbox.com/developers/apps) to create a App.

After created a App, you can find the APP_KEY and APP_SECRET, ACCESS_TYPE is also needed.

PATH_TO_WATCH is the directory that sync with Dropbox.

#### run auth.py ####

	python auth.py

It will ask you open a link in Browser, and just do what Dropbox ask. Then you can get the token file.

#### run watching.py ####

	python watching.py

This will watch dir `PATH_TO_WATCH`, and any changes like `create`, `modify`, `delete` and `move` will change the file in Dropbox.

#### commands ####

Download all the files and start to watch the folder.

	python watching.py

Clean the sync folder (remove it) and re-download the latest files.

	python watching.py -c

Download the latest files but do not watch it. The script will exit after download the files.

	python watching.py -e

Watch but not download, will update file to server.

	python watching.py -r

### something you can do yourself ###

I wrote some super easy interface like upload, download, delete, move. After you get the token, you can do it in python command line like

	from uploader import upload
	upload(file_name, as_file_name)

or you can run the file like:

	python uploader.py file_to_upload as_file

So if this watching.py is not what you want, I think it's very easy to be the one you really need.

### My PI ###

I need to download some files in my PI, don't need to update or edit on PI. so I just need a cron running on watching.py -c.

soundbbg at gmail
