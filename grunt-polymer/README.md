Usage Example: In your host

	mkdir -p ~/Projects/Personal/polymerLab
	cd ~/Projects/Personal/polymerLab
	cd ~/Projects/Docker/grunt_polymer && docker build -t grunt_polymer .
	docker run --name polymerLab -p 9000:9000 -v ~/Projects/Personal/polymerLab:/home/project -i -t grunt_polymer
