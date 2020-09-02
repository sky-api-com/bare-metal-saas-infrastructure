install:
	kubectl apply --validate=false -f https://github.com/jetstack/cert-manager/releases/download/v0.16.1/cert-manager.yaml
	make config;

config:
	ACME_EMAIL="$(shell cat ../acme_email.txt)" \
		DNS_ZONE_NAME="$(shell cat ../dns_zone.txt | sed 's/\./-/g')" \
		DNS_ZONE="$(shell cat ../dns_zone.txt)" \
		envsubst < ClusterIssuer.yml | kubectl apply -f -

	DNS_ZONE_NAME="$(shell cat ../dns_zone.txt | sed 's/\./-/g')" \
		DNS_ZONE="$(shell cat ../dns_zone.txt)" \
		CLOUDLFARE_API_KEY="$(shell cat ../cloudflare_token.txt | base64)" \
		envsubst < Secret.yml | kubectl apply -f -

dev:	
	