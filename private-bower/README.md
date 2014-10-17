

	docker pull sesteva/private-bower
	docker run --name bower -d -p 5678:5678 sesteva/private-bower
	
	docker stop bower
	docker start bower
	sudo docker-enter bower /bin/bash
