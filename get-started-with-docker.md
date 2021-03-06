---
layout: doc
title:  "Get Started with Docker"
permalink: /docs/deployment-in-docker.html
---

Another way to get started with Eagle is to run with [docker](https://github.com/docker/docker) by one of following options:

* Pull latest eagle docker image from [docker hub](https://hub.docker.com/r/apacheeagle/sandbox/) directly:

        docker pull apacheeagle/sandbox

  Then run eagle docker image:
  
      docker run -p 9099:9099 -p 8080:8080 -p 8744:8744 -p 2181:2181 -p 2888:2888 -p 6667:6667 -p 60020:60020 \
        -p 60030:60030 -p 60010:60010 -d --dns 127.0.0.1 --entrypoint /usr/local/serf/bin/start-serf-agent.sh \
        -e KEYCHAIN= --env EAGLE_SERVER_HOST=sandbox.eagle.incubator.apache.org --name sandbox \
        -h sandbox.eagle.incubator.apache.org --privileged=true apacheeagle/sandbox:latest \
        --tag ambari-server=true
      docker run -it --rm -e EXPECTED_HOST_COUNT=1 -e BLUEPRINT=hdp-singlenode-eagle --link sandbox:ambariserver\
        --entrypoint /bin/sh apacheeagle/sandbox:latest -c /tmp/install-cluster.sh

* Build eagle docker image from source code with [eagle-docker](eagle-external/eagle-docker) tool.

         git clone https://github.com/apache/incubator-eagle.git
         cd incubator-eagle && ./eagle-docker boot