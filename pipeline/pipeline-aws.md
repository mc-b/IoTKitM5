### Cloud Umgebung mit AWS Amazon Linux 2

Wird das Beispiel in [AWS Academy](https://www.awsacademy.com/) ausgeführt, können nur AWS Images, z.B. Amazon Linux 2 verwendet werden.

Das macht die Installation komplexer, weil zuerst die Packetquellen von snap hinzugefügt werden müssen.

    #cloud-config
    users:
      - name: user1
        sudo: ALL=(ALL) NOPASSWD:ALL
        groups: users, admin
        home: /home/user1
        shell: /bin/bash
        lock_passwd: false
        plain_text_passwd: 'password'        
    # login ssh and console with password
    ssh_pwauth: true
    disable_root: false 
    runcmd:
      - cd /etc/yum.repos.d && wget https://people.canonical.com/~mvo/snapd/amazon-linux2/snapd-amzn2.repo
      - yum install -y snapd
      - systemctl start snapd
      - snap refresh
      - sudo snap install microk8s --classic
      - sudo snap install kubectl --classic  
      - sudo mkdir -p /home/user1/.kube
      - sudo usermod -a -G microk8s user1
      - sudo chown -f -R user1 /home/users1/.kube 
      - su - user1 -c "microk8s enable dns ingress"
      - su - user1 -c "microk8s config" >/home/user1/.kube/config
      - sudo yum install -y curl git unzip
      - sudo mkdir /data
      - sudo chmod -R o=u,g=u /data  
      - sudo chmod 777 /data 
      - su - user1 -c "kubectl apply -f https://raw.githubusercontent.com/mc-b/lernkube/master/data/DataVolume.yaml"
      - su - user1 -c "kubectl apply -f https://raw.githubusercontent.com/mc-b/duk/master/addons/dashboard-skip-login-no-ingress.yaml"
      - su - user1 -c "(cd /tmp; git clone https://github.com/mc-b/mlg; cd mlg; kubectl apply -f jupyter/jupyter-mlg.yaml; cp -rpv data/* /data/ )"
      - su - user1 -c "kubectl apply -f https://raw.githubusercontent.com/mc-b/duk/master/iot/mosquitto.yaml"
      - su - user1 -c "kubectl apply -f https://raw.githubusercontent.com/mc-b/duk/master/kafka/zookeeper.yaml"
      - su - user1 -c "kubectl apply -f https://raw.githubusercontent.com/mc-b/duk/master/kafka/kafka.yaml"
      - su - user1 -c "kubectl apply -f https://raw.githubusercontent.com/mc-b/iot.kafka/master/iot-kafka-alert.yaml"
      - su - user1 -c "kubectl apply -f https://raw.githubusercontent.com/mc-b/iot.kafka/master/iot-kafka-consumer.yaml"
      - su - user1 -c "kubectl apply -f https://raw.githubusercontent.com/mc-b/iot.kafka/master/iot-kafka-pipe.yaml"
      - su - user1 -c "kubectl apply -f https://raw.githubusercontent.com/mc-b/duk/master/iot/nodered-kafka.yaml"
      - su - user1 -c "kubectl apply -f https://raw.githubusercontent.com/mc-b/misegr/master/bpmn/camunda.yaml"


