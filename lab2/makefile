# Set default no argument goal to help
.DEFAULT_GOAL := help

# Ensure that errors don't hide inside pipes
SHELL         = /bin/bash
.SHELLFLAGS   = -o pipefail -c

# Variables initialization from .env file
DC_PROJECT?=$(shell cat .env | grep COMPOSE_PROJECT_NAME | sed 's/^*=//')
APP_URL?=$(shell cat .env | grep VIRTUAL_HOST | sed 's/.*=//')
CURRENT_DIR?= $(shell pwd)

# Every command is a PHONY, to avoid file naming confliction -> strengh comes from good habits!
.PHONY: help
help:
	@echo "=================================================================================="
	@echo "        Secure HTTPS reverse proxy based on SWAG, Portainer and Authelia  "
	@echo "       >> https://github.com/elasticlabs/https-nginx-proxy-docker-compose"
	@echo " "
	@echo " Hints for developers:"
	@echo "  make up            # With working proxy, brings up the software stack"
	@echo "  make down          # Brings the Bubble stack down. "
	@echo "  make update        # Update the whole stack"
	@echo "  make cleanup       # /!\ Remove images, containers, networks, volumes & data"
	@echo "=================================================================================="

.PHONY: build
build: pull
	@echo "[Make] Build the stack"
	docker compose -f docker-compose.yaml build

.PHONY: pull
pull:
	@echo "[Make] Pull the stack images"
	docker compose -f docker-compose.yaml pull

.PHONY: up
up:
	@echo "[Make] Bringing up the stack images"
	docker compose -f docker-compose.yaml up

.PHONY: update
update:
	@echo "[Make] Update the stack images"
	docker compose -f docker-compose.yaml update