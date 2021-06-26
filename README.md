dudefellah.kafka_broker
=========

Install and configure a kafka broker (and only a kafka broker - you should have
zookeeper installed already).

Requirements
------------

No special requirements exist to run this role, but you will need an installed
an configured Zookeeper cluster before installing Kafka.

Role Variables
--------------

Role variables are listed and described in [defaults/main.yml](defaults/main.yml).

Dependencies
------------

None. See the note under [#requirements](Requirements).

Example Playbook
----------------

A simple example of installing and configuring a kafka cluster:

    - hosts: kafka_brokers
      tasks:
        - block:
            - name: Install kafak
              include_role:
                name: dudefellah.kafka_broker
              vars:
                # Let's not do this in production
                kafka_broker_user: root
                kafka_broker_group: root

                kafka_broker_zookeeper_client_port: 2181
                kafka_broker_listener_port: 9092
                kafka_broker_zookeeper_connect:
                  - zk1.example.com:2181
                  - zk2.example.com:2181
                  - zk3.example.com:2181

                kafka_broker_listener_security_protocol_map:
                  - BROKER0:SSL
                  - BROKER1:SSL
                  - BROKER2:SSL

                kafka_broker_log_dirs: /var/log/kafka
                ...

          become: true

License
-------

GPLv2+

Author Information
------------------

Dan - github.com/dudefellah
