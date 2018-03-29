# Decentralized system for Cashless payment
## Hyperledger Fabric Event Consortium

### Prerequisites 

This project sets the foundations of the Hyperledger Fabric network used in the development of the Cashless Payment project.

It is based on the Hyperledger Fabric ["Build Your First Network"](http://hyperledger-fabric.readthedocs.io/en/latest/build_network.html) tutorial.

To be able to launch the network sucessfully, the following prerequisites are needed. A complete installation procedure is available ["Here"](http://hyperledger-fabric.readthedocs.io/en/latest/prereqs.html). The following needs to be installed:

- **Docker** version 17.06.2-ce or greater
- **Go programming language** 1.9.X or greater
- **Node.js** Runtime and **NPM**
    - Node.js version 8.9.X or greater
    - NPM version 5.6.0 or greater
- **Python 2.7**
- Extra configuration for Windows is needed. See ["Here"](http://hyperledger-fabric.readthedocs.io/en/latest/prereqs.html#windows-extras)

### Installation

Once the prerequisites are installed, binaries and images need to be downloaded and installed on the machine. For Hyperledger version 1.1.0, run the following command:

`curl -sSL https://goo.gl/6wtTN5 | bash -s 1.1.0`

this will download all platform-specific binaries needed to set up the network:

- `cryptogen`
- `configtxgen`
- `configtxlator`
- `peer`
- `orderer`
- `fabric-ca-client`

For convenience, add the bin to the PATH:

`export PATH=<path to download location>/bin:$PATH`

Finally, move into the `fabric` folder and run the `build-network.sh` file twice:
- `./build-network.sh -m generate` to generate the cryptographic material
- `./build-network.sh -m up -s couchdb` to start the network on docker containers
- `./build-network.sh -m composer-generate` Generate PeerAdmin card
- `./build-network.sh -m composer-start` Start Composer runtime and deploy BNA

Once you are done developing, run the following command to clean up your environment:

`./build-network.sh -m down`

### Network Topology

The network is composed of:
- two Organizations that have 2 peers each. One organization is the Central Bank, the other organization is called Org1. Other organizations can be added to the network at a later point.
    - `peer0.centralbank.event-consortium.com`
    - `peer1.centralbank.event-consortium.com`
    - `peer0.org1.event-consortium.com`
    - `peer1.org1.event-consortium.com`
- A "Solo" ordering service: `orderer.event-consortium.com`

## Access state database (CouchDB) - DEV only

> If you choose to implement mapping of the fabric-couchdb container port to a host port, please make sure you are aware of the security implications. Mapping of the port in a development environment makes the CouchDB REST API available, and allows the visualization of the database via the CouchDB web interface (Fauxton). Production environments would likely refrain from implementing port mapping in order to restrict outside access to the CouchDB containers.

Run `http://localhost:5984/_utils` to access the CouchDB web interface (Fauxton)
