sudo docker run -e TEAMCITY_SERVER=http://172.17.42.1:8111 --name teamcity-agent_01 --link teamcity_server:teamcity_server -it sesteva/centos6-teamcity-agent-nodejs



