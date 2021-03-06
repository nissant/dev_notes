Docker Cheat Sheet

// Docker Commands
docker exec -it <container id> bash
docker attach <container id>
docker container ls
dockeer stop <container id>
dockeer kill <container id>
dockeer rm <container id>
docker container rm "id" --force

// Production Server Commands
docker build --add-host=gitlab-srv.transchip.com:106.199.15.49 --add-host=dlp2-wcg01.transchip.com:106.199.15.25 application-cis/dashboard-backend . 
docker run --name cis-dashboard-backend -d -p 8289:80 -v /stage/CIS_AUTO:/stage/CIS_AUTO --restart unless-stopped application-cis/dashboard-backend
docker run -d --restart unless-stopped --name esearch --net -v /mnt/local/elasticsearch/data:/usr/share/elasticsearch/data -p 9222:9200 9322:9300 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:7.6.1

// Backend Dev Server
docker exec -it dashboard-backend-dev bash
docker build -f Dockerfile_Dev -t dashboard-backend-dev .
docker run --name dashboard-backend-dev -d -p 8189:80 -v /stage/CIS_AUTO:/stage/CIS_AUTO --restart unless-stopped dashboard-backend-dev

// Frontend Dev Server
docker exec -it cis-dashboard-frontend-dev bash
docker build -f Dockerfile -t cis-dashboard-frontend-dev .
docker run --name cis-dashboard-frontend-dev -d -p 8489:80 -v /stage/CIS_AUTO:/stage/CIS_AUTO --restart unless-stopped cis-dashboard-frontend-dev

// Docker Reindex script
docker build -t es-indexer .
docker run -v /stage/CIS_AUTO:/stage/CIS_AUTO es-indexer hm1 reindex dark

// Misc
docker build -t rp .
docker run -it --rm rp
# The --rm option will clean up your container after use. It’s a good habit to use --rm to avoid filling up your system with stale Docker containers.




			  
