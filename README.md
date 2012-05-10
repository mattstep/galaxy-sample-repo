galaxy-sample-repo
==================
These instructions require ruby 1.9.3 (using rvm) and java 1.6

Grab the Galaxy CLI
===================
wget -O galaxy https://oss.sonatype.org/content/repositories/releases/com/proofpoint/galaxy/galaxy-cli/0.8/galaxy-cli-0.8-executable.jar
chmod 755 galaxy

Provision a local environment and use it
========================================
./galaxy environment provision-local --repository https://raw.github.com/mattstep/galaxy-sample-repo/master/ mygalaxy /tmp/mygalaxy/
./galaxy environment use mygalaxy

Install the sample server, show it, and start it
================================================
./galaxy install sample-server-0.63-distribution.tar.gz @sample-server-config-0.63.zip
./galaxy show
rvm use 1.9.3 #Gotta use ruby 1.9.3, so if you just got it, that's cool
./galaxy start --all

Do some stuff to the sample server
==================================
curl -X PUT -H'Content-Type:application/json' -d'{"email":"mattstep@mattstep.net", "name":"Matt Stephenson"}' localhost:8080/v1/person/mattstep
curl localhost:8080/v1/person
curl localhost:8080/v1/person/mattstep
curl -X DELETE localhost:8080/v1/person/mattstep

Bring it all down
=================
./galaxy stop --all
./galaxy terminate --all

