tutum-fedora
============

Simple Fedora docker image with SSH access


Usage
-----

To create the image `tutum/fedora` with one tag per Fedora release, execute the following commands on the tutum-fedora repository folder:

	docker build -t tutum/fedora:latest .

	docker build -t tutum/fedora:20 20

	docker build -t tutum/fedora:21 21


Running tutum/fedora
--------------------

Run a container from the image you created earlier binding it to port 2222 in all interfaces:

	sudo docker run -d -p 2222:22 tutum/fedora

The first time that you run your container, a random password will be generated
for user `root`. To get the password, check the logs of the container by running:

	docker logs <CONTAINER_ID>

You will see an output like the following:

	========================================================================
	You can now connect to this Fedora container via SSH using:

	    ssh -p <port> root@<host>
	and enter the root password 'U0iSGVUCr7W3' when prompted

	Please remember to change the above password as soon as possible!
	========================================================================

In this case, `U0iSGVUCr7W3` is the password allocated to the `root` user.

Done!

Setting a specific password for the root account
------------------------------------------------

If you want to use a preset password instead of a random generated one, you can
set the environment variable `ROOT_PASS` to your specific password when running the container:

	docker run -d -p 2222:22 -e ROOT_PASS="mypass" tutum/fedora


Adding authorized keys
----------------------

If you want to use ssh key for login, you can use `AUTHORIZED_KEYS` environment variable. The public keys are separated by `,`:

    docker run -d -p 2222:22 AUTHORIZED_KEYS="pubkey1, pubkey2, pubkey3" tutum/fedora:latest

If you put the corresponding private key under `~/.ssh/` where you run ssh command, you will not be asked to input the password.
