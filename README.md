# awselasticcache
Elastic Cache Demo

Prerequisites:
 --> Create a Security Group for EC2 instance - launch-wizard-15 with below inbound rules
      HTTP 80 0.0.0.0/0
      SSH 22 0.0.0.0/0
      TCP 5000 0.0.0.0/0  -> FOR FLASK APPLICATION
 --> Create another Security Group for Elastic Cache - elasticCacheSG with below inbound rules
      TCP 6379 launc-wizard-15  -> Allow request to port 6379 from the EC2 instance SG


--> Create a EC2 instance with Security Group launch-wizard-15
--> Create a Elastic Cache non clustered with SG elasticCacheSG
--> Make sure both the EC2 and Elastic Cache are in same VPC(use default one)
--> Connect to the EC2 instance using SSH or EC2 Instance Connect
      --> Install git - sudo yum install git -y
      --> Python will be installed by default
      --> Install pip  - curl -O https://bootstrap.pypa.io/get-pip.py
                       - python3 get-pip.py --user
      --> Install virtual environment - sudo pip install virtualenv
      --> Clone the repo - git clone https://github.com/ShalniGerald/awselasticcache.git
                         - cd awselasticcache/
      --> Activate vitualvenv - virtualenv venv
                              - source ./venv/bin/activate
                              - pip install -r requirements.txt
      --> Set the environment Variables - export REDIS_URL="redis://elastic-cache-demo.cm0aim.ng.0001.use1.cache.amazonaws.com:6379"
                                          export FLASK_APP=session-store.py
                                          export SECRET_KEY=some_random_value
      --> Run Flask App - flask run -h 0.0.0.0 -p 5000 --reload