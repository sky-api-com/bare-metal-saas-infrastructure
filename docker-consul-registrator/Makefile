it:
	make install CONSUL_KEY="$(shell cat consul_key.txt)" CONSUL_SERVER="$(shell cat consul_server_ip.txt)"

install:
	ansible-playbook -i inventory.txt main.yml -e CONSUL_ENCRYPTION_KEY=${CONSUL_KEY} -e CONSUL_SERVER=${CONSUL_SERVER}

dev:
	docker rm -f consul; true
	docker pull consul:latest
	docker run -d --name=consul -e CONSUL_BIND_INTERFACE=eth0 -e CONSUL_CLIENT_INTERFACE=eth0 consul agent -join=$(shell cat consul_server_ip.txt) -encrypt=$(shell cat consul_key.txt)
	sleep 2
	docker logs -f consul
	#docker ps
#docker exec -t consul sh -c "consul force-leave -prune \$(consul members|grep failed|cut -d ' ' -f1 | head -n1)"