## Nginx Proxy Manager DockSTARTer Override

This project is an override file that allows for [Nginx Proxy Manager](https://nginxproxymanager.com) to be integrated with the [dockSTARTer](https://github.com/GhostWriters/DockSTARTer) self-hosted server solution. 

## What is Nginx Proxy Manager?

Integrating Nginx Proxy Manager allows for the ability to aasily create forwarding domains, redirections, streams, reverse proxy configurations, and 404 hosts for Nginx. Additionally, it allows management for free SSL using Let's Encrypt or provide your own custom SSL certificates.

## What is dockSTARTer?

dockSTARTer is a an application focused on making it quick and easy to get up and running with Docker.  DS provides a library of user-selectable, self-hosted applications, and configures an integrated docker environment with the chosen software stack that allows for interoperability amongst the application containers.

## What are Overrides?

DS uses the docker-compose method of configuring each container for each application, with integrated global environment variables that are constant for all containers. The application dynamically creates the YAML-formatted configuration file based upon the user selections when running the DS application. This uses a file called docker-compose.yml.

DS gives the user additional control over customizing his application containers or adding additional applications that are not natively supported in the DS suite.  These overrides essentially are a layer over the standard docker-compose.yaml, and allow for changes to the original settings, without actually updating the dynamically-generated docker-compose.yaml file. These are configured in a file called docker-compose.override.yml.

## How do I Install?

Follow the [NGINX Proxy Manager](docs/npm-install.md) installation instructions.
