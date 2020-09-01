install: 
	ansible-playbook -i ./inventory.txt main.yml
	make connect

apply: connect
	cp ~/.kube/config-microdev ~/.kube/config
	kubectl apply -f hello-ingress/

connect:
	ssh $(shell cat master_ip.txt) "/snap/bin/microk8s config" > ~/.kube/config-microdev
	cp ~/.kube/config-microdev ~/.kube/config