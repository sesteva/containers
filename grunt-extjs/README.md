

Usage Example: In your host you would traditionally git clone a project first. The docker box will take care of running npm, bower and finally bring up the nodejs server.

	mkdir -p ~/Projects/Personal/extjsLab
	git clone .....
	cd ~/Projects/Personal/extjsLab
	docker pull sesteva/grunt-extjs
	docker run --name nameOfProject -p 9000:9000 -v ~/Projects/Personal/extjsLab:/home/project -i -t sesteva/grunt-extjs

If you dont have any yeoman project yet, then you should follow these steps instead:

	mkdir -p ~/Projects/Personal/extjsLab
	cd ~/Projects/Personal/extjsLab
	git pull sesteva/grunt-extjs
	docker run --name extjsLab -p 9000:9000 -v ~/Projects/Personal/extjsLab:/home/project -i -t sesteva/grunt-extjs /bin/bash

By passing a command at the end we override the CMD instructions the docker box has (npm install, bower install, grunt serve).

Now you can use yeoman to create the project, just execute the command 'yo' and follow the wizard. 

Next time you run the docker box the npm, bower and grunt instructions will take care of any updates.


