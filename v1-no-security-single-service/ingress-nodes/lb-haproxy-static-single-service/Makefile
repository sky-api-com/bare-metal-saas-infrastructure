it:
	make install SERVICE_NAME_IN_CONSUL="$(shell cat ../../consul_service_name.txt)"

install:
	ansible-playbook -i ../../inventory.txt main.yml -e SERVICE_NAME_IN_CONSUL=${SERVICE_NAME_IN_CONSUL}
