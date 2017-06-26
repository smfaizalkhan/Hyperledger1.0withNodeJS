# Hyperledger1.0withNodeJS

HyperLeder Fabric Samples with Node JS in Ubuntu

PreRequsites
 
  1) cURL 
          - Shipped along with Ubuntu
  2) Docker and Docker-compose
          a ) First way of instlaling docker
              - sudo apt-get update
              - sudo apt-get install docker-ce
     Installing docker will install the docker compose as well     
     
          b) Second Way of installing docker
          
              -  Issue the command
                  
                  Docker
                  wget -qO- https://get.docker.com/ | sh 
                  sudo service docker stop
                  nohup sudo docker daemon --api-cors-header="*" -H tcp://0.0.0.0:2375 -H unix:///var/run/docker.sock&
                  
                  Docker Compose
                  
                   curl -L https://github.com/docker/compose/releases/download/1.8.0/docker-compose-`uname -s`-`uname -m` >            /usr/local/bin/docker-compose
                  chmod +x /usr/local/bin/docker-compose
                  docker-compose --version
 3) Installing GO (Hyperledger 1.0 supports GO 1.7)
  
        -  wget https://storage.googleapis.com/golang/go1.7.4.linux-amd64.tar.gz
        -  sudo tar -xvf go1.7.4.linux-amd64.tar.gz
        
        Setting GO PATH
          
        -  export GOROOT = /home/faizal/go  (Given is my GOROOT,Please change as per your PATH)
        -  export GOPATH = $HOME/go
        -  export PATH = $PATH:$GOPATH/bin
    
     Restart the system for the PATHS toke effect or execute the command source ~/.profile
 
 4) Installing NodeJS (Hyperledger 1.0 supports NodeJS 6.9.x)
 
       - Download the .gz file from (https://nodejs.org/en/blog/release/v6.9.1/) as per OS
           I have done with  https://nodejs.org/dist/v6.9.1/node-v6.9.1-linux-x64.tar.xz
       - sudo tar -xvf node-v6.9.1-linux-x64.tar.xz
       - sudo mv node-v6.9.1-linux-x64.tar.xz /usr/lib/nodejs
       
         Setting NodeJS PATH
          
           - export NODEJS_HOME = /usr/lib/nodejs/node-v6.9.1-linux-x64 (Given is my GOROOT,Please change as per your PATH)
           - export PATH = $PATH:$GOPATH/bin:$NODEJS_HOME/bin:$PATH
  5) Clone this project by creating a folder fabric-sample
           
            - git clone https://github.com/hyperledger/fabric-samples.git
            - Navigate to fabcar (cd fabric-samples/fabcar)
            - Run the command ./startFabric.sh (sudo ./startFabric.sh)
                This script downloads and extracts the Fabric docker images having a 
                 
                  - peer node, ordering node, Certificate Authority and CLI container
                  - creates a channel and joins the peer to the channel
                  - installs smart contract onto the peer’s file system and instantiates said chaincode on the channel;      instantiate starts a chaincdoe container
                  - calls the initLedger function to populate the channel ledger with 10 unique cars
                  
                  Check the docker images (sudo docker images )and docker conatiners to check if the chaincode is installed (sudo docekr ps)
                   In our case we should have "fabcar-1.0" (chaincode name with version ) prefixed with peer name 
    
    6)  Now that chaincode is running in the network created we have to check it using client SDK (NodeJS)
        Navigate to  fabcar directory and issue the command "npm install" for the Node Package Manager to install the necessary 
         SDK node modules for the Client Modules
         this installs the main things such as fabric-client,path,util etc
    7) To check the invocation part issue "node query.js"
          This will give the list of CARS that is initialized during initilization of the chaincode (initLedger)
          
     8) To Create a new Asset in the Network we have to execute "node invoke.js"
     
           So we have to give the function to be invoked and args in the invoke.js
           
            fcn: 'createCar',
            args: ['CAR10', 'Chevy', 'Volt', 'Red', 'Nick'],
            
  PLease bring down the conatiner using docker-compose -f docker-compose.yml down 
   
    IF NOT NEXT TIME WHEN THE SCRIP RUNS WILL BE FACED WITH ERROR IN CREATING CHANNEL "BAD_REQ" which ia an indication of the channel already in existence
    
          
     
        
                
            
           
       
 
    

