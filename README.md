# OISF Docker Demo - Barcelona 2015

## Manually

### Suricata

    docker pull jasonish/suricata:beta

    docker run --name=suricata --net=host -v /var/log/suricata \
	    -it jasonish/suricata:beta -v -i eth0

### Elastic Search

    docker pull elasticsearch

	docker run --name elasticsearch \
		-v $(pwd)/data/elasticsearch:/usr/share/elasticsearch/data \
		-it elasticsearch --network.host 0.0.0.0

### Logstash

    docker pull logstash

	docker run --name logstash --volumes-from suricata \
        --link elasticsearch -v $(pwd)/config:/config \
	    logstash -f /config/logstash.conf

### Kibana

	docker pull kibana

	docker run --name kibana --link elasticsearch -p 5601:5601 kibana

### Add a Honeypot

    docker run --net=host -it honeynet/glastopf

## Docker Machine

	docker-machine create --driver digitalocean --digitalocean-size 4gb \
		--digitalocean-region fra1 \
		oisf-demo

# Notes

## Fedora 22 Setup
dnf -y install docker python-pip git tmux
pip install docker-compose
systemctl enable docker
systemctl restart docker
setenforce 0
git clone https://github.com/jasonish/oisf-docker-demo.git

## Docker Cleanup
docker stop $(docker ps -q)
docker rm $(docker ps -a -q)
docker rmi $(docker images -q)
