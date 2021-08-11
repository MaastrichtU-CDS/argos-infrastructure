# ARGOS Infrastructure

The ARGOS Fedederated Deep Learning Infrastructure is built from VANTAGE6 (priVAcy preserviNg federaTed leArninG infrastructurE for Secure Insight eXchange) infrastructure

For detailed understanding of the Vantage6 Infrastructure please refer to the documenentation [here](https://vantage6.ai/)

This repostitory provides instructions and scripts for installing the pre-requisites and setting up the infrastructure 

<img src="./Media/ARGOSINfra.jpg" width = 70% heigth=70% align="center">


## Prerequisites 

### Ubuntu 18.04 or any suitable Linux Distribution 
The partners are requested to install Ubuntu 18.04 or any higher version. Other Linux based distributions like CentOS and RedHat will work as well. 

### Docker Engine
Installing Docker is one of the pre-requisites for running a federated learning process using the infrastructure. You can follow the instructions for installing Docker [here](https://docs.docker.com/engine/install/ubuntu/). Alternately, you can run the shell script provided [here](./Scripts/install_Docker.sh).   

/// Insert Screenshot

### Python 3.6+
Pythton 3.6 or higher is required for smooth running of the software. Please follow the instructions [here](https://phoenixnap.com/kb/how-to-install-python-3-ubuntu) for installing Python3.6 or any higher version. 

Alternately, you can use the shell script provided to install python. 

/// Insert screenshot


N.B. The shell scripts work for Ubuntu distributions. For CentOS and Redhat distributions, please replace with suitable commands. 



## ARGOS Infrastructure Setup

The ARGOS Vantage6 Infrastructure setup consists of three components - a cental server, a aggregation node (also known as the master node) and multiple data nodes. As part of the consortium, the partners are required to install and setup only the Vantage6 Node Software. Our partner provider [Medical Data Works](https://www.medicaldataworks.com/) hosts the central [server](https://mdw-vantage6-argos.azurewebsites.net/apidocs/) and the aggregation node. 

### Install Python Virtual environment 

Installing python virtual environment is recommended but not mandatory. The below code installs, creates and activates the virtual enviroment named Vantage6

 ```
    sudo apt install python3-venv
    python3 -m venv vantage6
    source vantage6/bin/activate
``` 

### Install other dependencies 
Install python pip3 and check version

```
sudo apt update
sudo apt install python3-pip
pip3 --version
```

### Install and Setup Infrastructure
#### Node Software Installation 
The Vantage6 infrastructure has been modified to accomodate and will be installed withing the virtual enviroment Vantage6. 

``` pip3 install git+https://github.com/iknl/vantage6.git@feature/maastro-n2n-communication```  or
``` pip3 install -r requirements.txt```


#### Node Setup 
At this point, we are ready to setup a new node. At the terminal type ```vnode new``` and follow the instructions. For setting the node, you will require specfic information from the server admin. The node software needs the **server url** and a **api_key** to authenticate with the server [Please contact over email for obtaining the api_key]


<img src="./Media/cli.JPG" width = 70% heigth=70%>

On successful completion, a configuration file(.yaml) will be created. This configuration file holds the key information necessary for all further communication between the node and the server. 

#### Additional environment variables in the configuration file
Add the following environment variables in the configuration file by using the vi command
- public_ip : keep the value blank
- api_forwarder_port  : the default port value is 5555 

``` 
    vnode files
    vi [/location/to/configurationFile.yaml]
 ```

<img src="./Media/configuration.JPG" width = 70% heigth=70%>

To start the node type at the terminal 

``` vnode start --port 3030 --image harbor2.vantage6.ai/infrastructure/maastro-node --attach ```

<img src="./Media/nodestart.JPG" width = 70% heigth=70%>

The node is up for receiving tasks from the server
