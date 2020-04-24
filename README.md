![Atlassian Confluence Server](https://wac-cdn.atlassian.com/dam/jcr:5d1374c2-276f-4bca-9ce4-813aba614b7a/confluence-icon-gradient-blue.svg?cdnVersion=696)

Confluence Server is where you create, organise and discuss work with your
team. Capture the knowledge that's too often lost in email inboxes and shared
network drives in Confluence - where it's easy to find, use, and update. Give
every team, project, or department its own space to create the things they need,
whether it's meeting notes, product requirements, file lists, or project plans,
you can get more done in Confluence.

Learn more about Confluence Server: <https://www.atlassian.com/software/confluence>

# Overview

This Docker container makes it easy to get an instance of Confluence up and
running.

# Quick Start

For the directory in the environmental variable `CONFLUENCE_HOME` that is used
to store Confluence data (amongst other things) we recommend mounting a host
directory as a [data volume][1].

Start Atlassian Confluence Server:

    docker run -v /data/your-confluence-home:/var/atlassian/application-data/confluence --name="confluence" -d -p 8090:8090 -p 8091:8091 geeoz/atlassian-confluence


**Success**. Confluence is now available on <http://localhost:8090>*

Please ensure your container has the necessary resources allocated to it.
We recommend 2GiB of memory allocated to accommodate the application server.
See [Supported Platforms][2] for further information.

_* Note: If you are using `docker-machine` on Mac OS X, please use `open http://$(docker-machine ip default):8090` instead._

# Configuring Confluence

This Docker image is intended to be configured from its environment; the
provided information is used to generate the application configuration files
from templates. Most aspects of the deployment can be configured in this manner; 
the necessary environment variables are documented below.

You can configure a small set of things by supplying the following environment variables

| Environment Variable              | Description |
| --------------------------------- | ----------- |
| CATALINA_CONNECTOR_PROXYNAME      | The reverse proxy's fully qualified hostname. |
| CATALINA_CONNECTOR_PROXYPORT      | The reverse proxy's port number via which Confluence is accessed. |
| CATALINA_CONNECTOR_SCHEME         | The protocol via which Confluence is accessed. |
| CATALINA_CONNECTOR_SECURE         | Set 'true' if CATALINA_CONNECTOR_SCHEME is 'https'. |
| CATALINA_CONTEXT_PATH             | The context path the application is served over. |
| JAVA_OPTS                         | The standard environment variable that some servers and other java apps append to the call that executes the java command. |
| CROWD_ENABLE                      | Enable Crowd Integration and SSO |
| APPLICATION_NAME                  | The name that the application will use when authenticating with the Crowd server. |
| APPLICATION_PASSWORD              | The password that the application will use when authenticating with the Crowd server. |
| APPLICATION_LOGIN_URL             | Crowd will redirect the user to this URL if their authentication token expires or is invalid due to security restrictions. |
| CROWD_SERVER_URL                  | The URL to use when connecting with the integration libraries to communicate with the Crowd server. |
| CROWD_BASE_URL                    | The URL used by Crowd to create the full URL to be sent to users that reset their passwords. |
| SESSION_ISAUTHENTICATED           | The session key to use when storing a Boolean value indicating whether the user is authenticated or not. |
| SESSION_TOKENKEY                  | The session key to use when storing a String value of the user's authentication token. |
| SESSION_VALIDATIONINTERVAL        | The number of minutes to cache authentication validation in the session. If this value is set to 0, each HTTP request will be authenticated with the Crowd server. |
| SESSION_LASTVALIDATION            | The session key to use when storing a Date value of the user's last authentication. |
You can read more about optional settings in the [crowd.properties](https://confluence.atlassian.com/crowd/the-crowd-properties-file-98665664.html) file.

[1]: https://docs.docker.com/userguide/dockervolumes/#mount-a-host-directory-as-a-data-volume
[2]: https://confluence.atlassian.com/display/DOC/Supported+platforms
