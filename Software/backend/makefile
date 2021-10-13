GH_REPO = https://github.com/JKUATSES/2021-project-hack.git
C_DIR = chronograf/
I_DIR = influxdb/
K_DIR = kapacitor/
G_DIR = grafana/

clean: stop remove-files

all: clean pull build start

# This pull the images for the docker images
pull:
	docker-compose pull
# This builds any images which are supposed to be built while running docker compose
build:
	docker-compose build
# This starts up the containers. We change the read and write rights for the rabbitmq file the start it up
start:
	chmod 755 rabbitmq/cluster-entrypoint.sh
	docker-compose up -d
# This stops the containers while maintaining their volumes
stop:
	docker-compose down
# This prunes the images containers, volumes and networks. It also removes the data files that were created when the docker containers spinned up to existence
remove-files:
	docker system prune -a
	docker volume prune
	[ -d $(C_DIR) ] && echo exists && rm -rf $(C_DIR) $(I_DIR) $(K_DIR) || echo not exists

# This watches the conatiner logs
logs:
	watch docker-compose logs
# Removes the data bases and creates new directories
clear_db:
	sudo rm -rf $(C_DIR)/data $(G_DIR)/data $(G_DIR)/provisioning $(I_DIR)/data $(K_DIR)/data elasticsearch/data logstash/data kibana/data
	mkdir $(K_DIR)/data $(C_DIR)/data $(I_DIR)/data elasticsearch/data logstash/data kibana/data
