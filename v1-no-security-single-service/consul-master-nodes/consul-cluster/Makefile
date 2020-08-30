it:
	make install CONSUL_KEY="$(shell cat ../../consul_key.txt)"

install:
	ansible-playbook -i ../../inventory.txt main.yml -e consul_encryption_key=${CONSUL_KEY}

keygen:
	test -f consul_key.txt || echo $$(consul keygen) > consul_key.txt