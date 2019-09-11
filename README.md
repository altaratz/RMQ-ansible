# RMQ-ansible
rabbitmq:

Ansible playbooks for creating Ubuntu/Debian RabbitMQ nodes.

Playbooks:

create_vms.yml: Creates a set of RabbitMQ nodes using a specified template in a vSphere environment.

rabbitmq.yml: Configures a set of Ubuntu/Debian nodes as a RabbitMQ cluster


In both create_vms.yml & rabbitmq.yml when you see the "{{ item }}" variable please adjust properly in the rabbitmq-vars.yml file
