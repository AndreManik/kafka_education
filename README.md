1. deploy containers
    > docker-compose up -d (-d is optional)

2. check the containera is up and running
    > docker ps --format "{{.Names}}: {{.State}}: {{.Networks}} : {{.Ports}}"
    >
    >> kafkaBroker2: running: kafka-networks : 0.0.0.0:9093->9093/tcp, 0.0.0.0:9201->9201/tcp, 9092/tcp, 0.0.0.0:29093->29093/tcp
    >> kafkaBroker3: running: kafka-networks : 0.0.0.0:9094->9094/tcp, 0.0.0.0:9301->9301/tcp, 9092/tcp, 0.0.0.0:29094->29094/tcp
    >> kafkaBroker1: running: kafka-networks : 0.0.0.0:9092->9092/tcp, 0.0.0.0:9101->9101/tcp, 0.0.0.0:29092->29092/tcp
    >> zookeeper: running: kafka-networks : 2888/tcp, 0.0.0.0:2181->2181/tcp, 3888/tcp

3. connect to the one of the containers to use kafka cli commands
    > docker exec -it kafkaBroker1 bash

4. base commands for create topic
    * create topic
        > kafka-topics --create --bootstrap-server kafkaBroker1:29092 --topic example1 --partitions 3 --replication-factor 3
        in case of unable to establish connection with one of the broker, can connect to the broker and try again
    * get list of the topics
        > kafka-topics --list --bootstrap-server kafkaBroker1:29092
    * topic details
        > kafka-topics --bootstrap-server kafkaBroker1:29092 --describe --topic example1

        > Topic: example1 TopicId: 2NngRO4uSJyRAR_Bif_cug PartitionCount: 3       ReplicationFactor: 3    Configs: 
            >> Topic: example1 Partition: 0    Leader: 2       Replicas: 2,1,3 Isr: 2,1,3
            >> Topic: example1 Partition: 1    Leader: 3       Replicas: 3,2,1 Isr: 3,2,1
            >> Topic: example1 Partition: 2    Leader: 1       Replicas: 1,3,2 Isr: 1,3,2

5. base commands for work with messages
    * send message to topic
        > kafka-console-producer --bootstrap-server kafkaBroker1:29092 --topic example1
            and write the messagges

    * read the message
        > kafka-console-consumer --bootstrap-server kafkaBroker1:29092 --topic example [--from-beginning]
    


