PROJ_NAME=hid-sp18-414

run-node1:
	python E516Chain.py -p 9999

run-node2:
	python E516Chain.py -p 8888

docker-build:
	docker build --network=host -t $(PROJ_NAME) .
docker-start-1:
	docker run -d -p 9999:9999 ${PROJ_NAME} run-node1
docker-start-2:
	docker run -d -p 8888:8888 ${PROJ_NAME} run-node2
docker-stop:
	docker stop $$(docker ps -a -q --filter ancestor=$(PROJ_NAME))

requirements:
	pip install -r requirements.txt

test:
	curl -H "Content-Type: application/json"  \
		-X POST \
		-d '{"nodes": ["http://127.0.0.1:8888"]}' \
		http\://localhost\:9999/register

	curl -H "Content-Type: application/json"  \
		-X POST \
		-d '{"nodes": ["http://127.0.0.1:9999"]}' \
		http\://localhost\:8888/register

	curl -H "Content-Type: application/json" \
		-X GET \
		http\://localhost\:8888/consensus
	
	curl -H "Content-Type: application/json" \
		-X GET \
		http\://localhost\:8888/chain

	curl -H "Content-Type: application/json"  \
		-X POST \
		-d '{"sender": "82eab15187ee92c6cd394edd974e", "receiver": "d4ee26sse15109ee92c6csd94fgd9745", "amount": 7}' \
		http\://localhost\:8888/newtransaction
	
	curl -H "Content-Type: application/json" \
		-X GET \
		http\://localhost\:8888/mine

	curl -H "Content-Type: application/json" \
		-X GET \
		http\://localhost\:9999/consensus

	curl -H "Content-Type: application/json"  \
		-X POST \
		-d '{"sender": "d4ee26sse15109ee92c6csd94fgd9745", "receiver": "82eab15187ee92c6cd394edd974e", "amount": 2}' \
		http\://localhost\:9999/newtransaction

	curl -H "Content-Type: application/json"  \
		-X POST \
		-d '{"sender": "d4ee26sse15109ee92c6csd94fgd9745", "receiver": "82eab15187ee92c6cd394edd974e", "amount": 8}' \
		http\://localhost\:9999/newtransaction
	
	curl -H "Content-Type: application/json" \
		-X GET \
		http\://localhost\:9999/mine

	curl -H "Content-Type: application/json" \
		-X GET \
		http\://localhost\:8888/consensus
	
	curl -H "Content-Type: application/json" \
		-X GET \
		http\://localhost\:8888/chain
	
		