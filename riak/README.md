# seven-databases - RIAK

Put the instructions etc for the team here

# Builds

Dev tools, which are automatically installed by the vagrant build

https://github.com/basho/riak-client-tools/tree/master/devrel

A development cluster is automativally built for you, with four nodes. To check, test etc, follow the instructions below:

Check installation of cluster
```
$ cd Projects/basho/riak/dev
$ cd ls
```
You should see dev1, dev2 etc

Start
```
$ dev1/bin/riak start
```
…. or
```
$ for node in dev*; do sudo $node/bin/riak start; done
```

Check
```
$ ps aux | grep beam
$ for node in dev*; do sudo $node/bin/riak ping; done
```

Create cluster
```
$ for n in {2..4}; do sudo dev$n/bin/riak-admin cluster join dev1@127.0.0.1; done
$ sudo dev1/bin/riak-admin cluster plan
$ sudo dev2/bin/riak-admin cluster commit
```

Testing the cluster
```
$ sudo dev1/bin/riak-admin member-status
$ curl -XPUT http://localhost:10018/buckets/welcome/keys/german -H 'Content-Type: text/plain' -d 'herzlich willkommen'
```

Your HTTP port might differ, so check your configuration files for the valid port in your cluster. That information can be found in /etc/riak.conf if you're using the newer configuration system or in /etc/app.config if you're using the older system.
```
$ curl http://localhost:10018/buckets/welcome/keys/german
```


# WARNING - IGNORE THE STUFF BELOW

## Install Riak from Source
Failed on canola pam header, needed:
```
$ sudo apt-get install libpam0g-dev
```


Check
```
$ cd dev;ls
```

Start
```
$ dev1/bin/riak start
```
…. or
```
$ for node in dev*; do $node/bin/riak start; done
```

Check
```
$ ps aux | grep beam
$ for node in dev*; do $node/bin/riak ping; done
```

Create cluster
```
$ for n in {2..5}; do dev$n/bin/riak-admin cluster join dev1@127.0.0.1; done
$ dev1/bin/riak-admin cluster plan
$ dev2/bin/riak-admin cluster commit
```

Testing the cluster
```
$ dev1/bin/riak-admin member-status
$ curl -XPUT http://localhost:10018/buckets/welcome/keys/german -H 'Content-Type: text/plain' -d 'herzlich willkommen'
```

Your HTTP port might differ, so check your configuration files for the valid port in your cluster. That information can be found in /etc/riak.conf if you're using the newer configuration system or in /etc/app.config if you're using the older system.
```
$ curl http://localhost:10018/buckets/welcome/keys/german
```

# General instructions

Updated hotel.rb to fix Riak version change issues. You may need to adjust the port number.

# Install OSX Dev Cluster
## Quick start development cluster when all else fails
```
$ git clone git://github.com/basho/riak-dev-cluster.git
$ cd riak-dev-cluster
$ rake bootstrap
$ rake member_status
```