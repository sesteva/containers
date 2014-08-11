Usage Example: In your host

	mkdir -p ~/Projects/Personal/muzza
	cd ~/Projects/Personal/muzza
	git clone https://github.com/unexpectedprofit-org/muzza.git
	cd ~/Projects/Docker/grunt_angular && docker build -t grunt_angular .
	docker run --name muzza -p 9000:9000 -v ~/Projects/Personal/muzza:/home/project -i -t grunt_angular
