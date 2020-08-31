install:
	ansible-playbook -i ../../inventory.txt main.yml \
		-e CLOUDFLARE_DNS_API_TOKEN="$(shell cat ../../cloudflare_token.txt)" \
		-e HTTPS_DOMAIN="${shell cat ../../domain.txt}" \
		-e ACME_EMAIL="${shell cat ../../acme_email.txt}" 

dev:
	chmod 600 ./templates/acme.json
	docker rm -f traefik; true
	docker rm -f tutum; true
	docker run -d -p 8085:80 --name tutum tutum/hello-world
	docker run --name traefik -p 8081:8081 --link tutum:tutum --link consul:consul \
		-p 8080:8080 \
		-p 443:443 \
		-it \
		-e CLOUDFLARE_DNS_API_TOKEN="$(shell cat ../../cloudflare_token.txt)" \
		-v $$(pwd)/templates/traefik.toml:/etc/traefik/traefik.toml \
		-v $$(pwd)/templates/acme.json:/var/acme.json \
		-v $$(pwd)/templates/provider.toml:/etc/traefik/fileProvider/provider.toml \
		traefik:v2.3 

cert:
	curl --insecure -vvI -H Host:hostname https://127.0.0.1:443 2>&1 | awk 'BEGIN { cert=0 } /^\* SSL connection/ { cert=1 } /^\*/ { if (cert) print }'
	curl --insecure -H Host:hostname https://127.0.0.1:443