IM - Infrastructure Manager client
==================================

IM is a tool that ease the access and the usability of IaaS clouds by automating
the VMI selection, deployment, configuration, software installation, monitoring
and update of Virtual Appliances. It supports APIs from a large number of
virtual platforms, making user applications cloud-agnostic. In addition it
integrates a contextualization system to enable the installation and
configuration of all the user required applications providing the user with a
fully functional infrastructure.

```
usage: client.py [-u|--xmlrpc-url <url>] [-a|--auth_file <filename>] operation op_parameters
```

Authentication File:

The authorization data is used to validate access to the components in the
infrastructure. This file is composed of a set of "key - value" pairs,
where the user specifies the authorization data for all the components and cloud
deployments available. File auth.dat shows examples of authorization data.

The list of "key" values that must be specified for each component are:

* id: An optional field used to identify the virtual deployment. It must be unique
      in the authorization data.
* type: The type of the component. It can be any of the components of the
        architecture, such as the "InfrastructureManager", "VMRC" or any of
        the cloud deployments currently supported by the IM: OpenNebula, EC2,
        OpenStack, OCCI or LibVirt.
* username: The name of the user for the authentication. In the EC2 and OpenStack
            cases it refers to the Access Key ID value. password: The password for
            the authentication. In the EC2 and OpenStack cases it refers to the
            Secret Access Key value.
* host: The address to the server in format "address:port" to specify the cloud
        deployment to access. In the EC2 and in the system components (IM and VMRC)
        this field is not used.

To avoid typing the parameters in all the client calls. The user can define a config
file "im_client.cfg" in the current directory or a file ".im_client.cfg" in their 
home directory. In the config file the user can specify the following parameters:

```
[im_client]
xmlrpc_url=http://localhost:8899
auth_file=auth.dat
xmlrpc_ssl=no
xmlrpc_ssl_ca_certs=/tmp/pki/ca-chain.pem
```

1. INSTALLATION
===============

1.1 REQUISITES
--------------

IM is based on python, so Python 2.4 or higher runtime and standard library must
be installed in the system.

It is also required to install the Python Lex & Yacc library (http://www.dabeaz.com/ply/).
It is available in all of the main distributions as 'python-ply' package.

1.2 OPTIONAL PACKAGES
--------------

In case of using the SSL secured version of the XMLRPC API the SpringPython
framework (http://springpython.webfactional.com/) must be installed.

1.3 INSTALLING
--------------

You only need to install the tar-gziped file to any directoy:

```
$ tar xvzf IM-client-X.XX.tar.gz
```

1.4 CONFIGURATION
--------------

Adjust the parameters in $CLIENT_PATH/config.py. Please pay attention to the next 
configuration variables, as they are the most important

* CLIENT_DIR - must be set to the full path where the IM client is installed 
            (e.g. /usr/local/im-client)
         
### 1.4.1 SECURITY

Security is disabled by default, but it should be taken into account that it would
be possible that someone that has local network access can "sniff" the traffic and
get the messages with the IM with the authorisation data with the cloud providers.

I can be activated both in the XMLRPC and REST APIs. Setting this variables:

```
XMLRCP_SSL = True
```

And then set the variables: XMLRCP_SSL_CA_CERTS to your CA certificates paths.


