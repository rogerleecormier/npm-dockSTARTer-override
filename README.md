# docSTARTer-overrides
This project is merely a collection of overrides for the [dockSTARTer](https://github.com/GhostWriters/DockSTARTer) application, also known as "DS.  

# What is dockSTARTer?
dockSTARTer is a an application focused on making it quick and easy to get up and running with Docker.  DS provides a library of user-selectable, self-hosted applications, and configures an integrated docker environment with the chosen software stack that allows for interoperability amongst the application containers.

# What are Overrides?
DS uses the docker-compose method of configuring each container for each application, with integrated global environment variables that are constant for all containers. The application dynamically creates the YAML-formatted configuration file based upon the user selections when running the DS application. This uses a file called docker-compose.yml. 

DS gives the user additional control over customizing his application containers or adding additional applications that are not natively supported in the DS suite.  These overrides essentially are a layer over the standard docker-compose.yaml, and allow for changes to the original settings, without actually updating the dynamically-generated docker-compose.yaml file. These are configured in a file called docker-compose.override.yml. 

# My Overrides
This repository is merely a selection of overrides that I use to enhance my DS implementation.  They were created for my personal use, but are posted for others to review and use if they choose. Some of these may be submitted to DS for review to become updates or additions to the current DS suite of applications.

 <!--- - [NGINX Proxy Manager](doc/INSTALL.md) --->
