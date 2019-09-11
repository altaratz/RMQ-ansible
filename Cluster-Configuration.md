How to config rabbitmq server cluster:

Edit /etc/hosts:

vi /etc/hosts

#10.180.138.47  rabbitmq-1

#10.180.138.48  rabbitmq-2

#10.180.138.49  rabbitmq-3

#10.180.138.50  rabbitmq-4

#10.180.138.51  rabbitmq-5



Restart rabbitmq-server [all nodes]:

service rabbitmq-server restart

Enable rabbitmq-server service:

chkconfig rabbitmq-server on


Verify rabbitmq-server is running [all nodes]:

rabbitmqctl status



Add User:

$ sudo rabbitmqctl add_user "myuser" "mypassword"

$ sudo rabbitmqctl set_user_tags "myuser" administrator

$ sudo rabbitmqctl set_permissions -p / "myuser" ".*" ".*" ".*"


Create rabbitmq-server cluster:

Step 1:

view /var/lib/rabbitmq/.erlang.cookie [rabbitmq-1]

[rabbitmq-1]

cat /var/lib/rabbitmq/.erlang.cookie

"Result = AFYDPNYXGNARCABLNENP"


Step 2:

set cookie same node 1 (Make sure the erlang cookies are the same all node.) [Node 2-5]

[Node 2-5]

service rabbitmq-server stop

echo -n "AFYDPNYXGNARCABLNENP" > /var/lib/rabbitmq/.erlang.cookie

service rabbitmq-server start


Step 3:

join cluster to rabbitmq-1 [Node 2-5]

[Node 2-5]

rabbitmqctl stop_app

rabbitmqctl reset

rabbitmqctl join_cluster rabbit@rabbitmq-1

rabbitmqctl start_app

Verify rabbitmq-server cluster [all nodes]

rabbitmqctl cluster_status

