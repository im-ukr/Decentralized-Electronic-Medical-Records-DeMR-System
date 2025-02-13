# Decentralized Electronic Medical Record (DeMR) System using Hyperledger Fabric

The content of this README.md file as per the following headers:<br><br>
<b>A. Introduction <br>
B. Installation <br>
C. Set-up <br>
D. Steps to successfully close and re-run the project <br>
E. Version Used <br></b>

## A. Introduction

This project marks a significant advancement by successfully integrating blockchain technology into Electronic Health Records (EHRs). The primary objective is to enhance the security and privacy of patient data through blockchain’s decentralized structure, ensuring data integrity and protection against unauthorized modifications.
This repository provides the necessary scripts and configurations for establishing a Hyperledger Fabric network and deploying chaincode.

## B. Installation
The following installations are preferred:
- Ubuntu 20.04+/ MacOS/ Ubuntu running on WSL2 (For Windows)
- Docker and WSL extension on Visual Studio Code
- Docker Desktop (If using WSL2 then ensure that WSL integration with Ubuntu is enabled under Docker desktop settings)
- Python 3 (for serving frontend via http.server)
- Node.js and nvm. (Check the versions mentioned at the end of this readme)

## C. Setup

1. **Clone the repository:**

   ```bash
   git clone https://github.com/im-ukr/Decentralized-Electronic-Medical-Records-DeMR-System.git
   ```
   Navigate into the project folder:
    ```bash
   cd EMR-Management-System-using-Hyperledger-Fabric
   ```
   And then run these command:
    ```bash
   curl -sSLO https://raw.githubusercontent.com/hyperledger/fabric/main/scripts/install-fabric.sh
   chmod +x install-fabric.sh
   ./install-fabric.sh docker binary
   ```

3. **Navigate to the test network directory:**

   ```bash
   cd fabric-samples/test-network
   ```
   
5. **Execute the following commands to set up the network and deploy the chaincode:**

   ```bash
   ./network.sh down
   ./network.sh up createChannel -ca -s couchdb
   ./deploymentScript.sh
   ```
   ### For errors (Skip if no issues; continue from Step 4):
   If facing any peer binaries issue when starting the network, follow these commands in this directory:
   ```bash
   curl -sSL https://bit.ly/2ysbOFE | bash -s
   ```
   Note where the peer binary is located using following command, **MODIIFY it according to the project location within your system.**
   ```bash
   find ~/BT-Project/EMR-Management-System-using-Hyperledger-Fabric -name peer
   ```
   Export it to the path based on the location, for example:
   ```bash
   export PATH=$PATH:/home/im-ukr/BT-Project/EMR-Management-System-using-Hyperledger-Fabric/fabric-samples/test-network/fabric-samples/bin
   ```
   Verify the peer version:
   ```bash
   peer version
   ```

6. **After the execution of the above commands, navigate to the backend-combined directory:**

   ```bash
   cd backend-combined
   ```

7. **Enroll admin, register user, and start the application:**

   Before enrolling, run this command:
   ```bash
   npm install fabric-ca-client
   ```
   ```bash
   node enrollAdmin.js
   node registerUser.js
   node app.js
   ```

8. **To view Frontend**

   Open a new terminal and run these commands:
   ```bash
   cd EMR-Management-System-using-Hyperledger-Fabric/fabric-samples/test-network/frontend
   python3 -m http.server
   ```

## D. Steps to successfully close and re-run the project:
To close the project, stop the backend as well as frontend terminal and execute the following command in test-network directory:
   ```bash
   ./network.sh down
   ```
For running again, execute the following commands only as per their respective directories (mentioned earlier):
   ```bash
   ./network.sh up createChannel -ca -s couchdb
   ./deploymentScript.sh
   ```
   ```bash
   node enrollAdmin.js
   node registerUser.js
   node app.js
   ```
To view frontend, open a new terminal and run these commands:
   ```bash
   cd EMR-Management-System-using-Hyperledger-Fabric/fabric-samples/test-network/frontend
   python3 -m http.server
   ```
## E. Used:
- Node v23.7.0 / v20.18.1
- npm v10.9.2 / v10.8.2
- nvm v0.39.5
- docker v27.4.0
