# OISF Docker Demo - Barcelona 2015

## Manually

### Suricata

    docker pull jasonish/suricata:beta

    docker run --name=suricata --net=host -v /var/log/suricata \
	    -it jasonish/suricata:beta -v -i enp3s0

### Logstash

    docker pull logstash

### Elastic Search

    docker pull elasticsearch

## Docker Machine

	docker-machine create --driver digitalocean --digitalocean-size 4gb \
		--digitalocean-region fra1 \
		oisf-demo
