# Dockerized Facebook Deepmask

## Deploy instuctions for AWS EC2
* Install Docker Machine: https://docs.docker.com/machine/
* Launch a GPU instance with specified AMI (ami-a65686c6 already has NVIDIA drivers compatible with g2.2xlarge):

  ```
  docker-machine create --driver amazonec2 \
                        --amazonec2-region us-west-2 \
                        --amazonec2-zone a \
                        --amazonec2-ami ami-a65686c6 \
                        --amazonec2-instance-type g2.2xlarge \
                        --amazonec2-vpc-id vpc-xxxxxxxx \
                        --amazonec2-access-key AKIAxxxxxxxxxxxxxxxx \
                        --amazonec2-secret-key xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx \
                        nvidia-docker-deepmask
  ```

  Launcher will create security group for SSH access
* SSH into instance and install several tools (nvidia-docker, docker-compose, nvidia-docker-compose):

  ```
  wget -P /tmp https://github.com/NVIDIA/nvidia-docker/releases/download/v1.0.0/nvidia-docker_1.0.0-1_amd64.deb
  sudo dpkg -i /tmp/nvidia-docker*.deb && rm /tmp/nvidia-docker*.deb
  sudo pip install docker-compose
  sudo pip install nvidia-docker-compose
  ```

* Clone this repo in the `/home/ubuntu` folder:

  ```
  cd /home/ubuntu
  git clone https://github.com/marvelousNinja/deepmask-investigation
  ```

* Now build the Docker image inside of `deepmask-investigation` folder:

  ```
  cd ./deepmask-investigation
  sudo nvidia-docker-compose build torch
  ```

## Usage
* Run the container from `deepmask-investigation` folder with:

  ```
  sudo nvidia-docker-compose run torch /bin/bash
  ```

* Use Deepmask with:

  ```
  # Outputs file into res.jpg
  th computeProposals.lua pretrained/deepmask -img /path/to/image.jpg
  ```

* `./output` folder is mounted in the container, so you can copy resulting files there

* You can copy files from the EC2 to your local machine with `docker-machine scp`:

  ```
  docker-machine scp nvidia-docker-deepmask:/home/ubuntu/deepmask-investigation/output/* .
  ```

## Useful Links
* https://github.com/facebookresearch/deepmask
* https://github.com/NVIDIA/nvidia-docker/wiki/Deploy-on-Amazon-EC2
