Usage Example: In your host

	mkdir -p ~/Projects/Personal/nameOfProject
	cd ~/Projects/Personal/nameOfProject
	git clone https://github.com/username/nameOfProject.git
	
	docker pull sesteva/grunt-angular
	docker run --name nameOfProject -p 9000:9000 -v ~/Projects/Personal/nameOfProject:/home/yeoman/project -i -t sesteva/grunt-angular
