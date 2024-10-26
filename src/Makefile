PATH := ${PATH};${HOME}/bin

.PHONY: help
help:
	@cat Makefile

remote/build:
	hugo

remote/sync:
	cp -rv public/* ${HOME}/www/temama.soy/
