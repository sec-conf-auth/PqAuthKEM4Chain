# PqAuthKEM4Chain
# About The Function of Chaincodes
The main implementation of the PQ user authentication and key
exchange system consists of two chaincodes, namely `PqCa` and
`PqUser`. The `PqCa` chaincode provides
APIs to generate the PQ key pairs together with the related
certificates (for the CA, the user identity key and the user KEM
key), query one certificate (based on a given serial number),
verify one certificate (and its parent certificates in the certificate
chain), revoke one certificate, encapsulate and decapsulate the
shared secret between users. While the `PqUser` chaincode
invokes the corresponding APIs in `PqCa` to query/verify one
certificate and provides APIs to perform the encapsulation and
decapsulation operations for the users.

The data structure in the off-chain private databases is
designed relatively simply for further development. In the off-
chain private databases (e.g., MySQL), one key pair, the
corresponding certificate and related information (e.g., password)
are all stored in one line, and the certificate serial number is set as
the key of the line.

# About The Function of Client Codes
Besides the chaincodes, we also develop client codes to help
developers create their applications based on the PQ user
authentication and key exchange system. 
There are two client codes, namely `PqCa_Cli` and `PqUser_Cli`,
which are written in Go and used to invoke the APIs in the
corresponding chaincodes. The configuration files(e.g.,connection-profile.yaml) for the client
codes to invoke the chaincodes are also provided.

# About The Use of Docker Image
In the experiments , we utilize the liboqs 0.6.0 library [1] together with its Go wrapper [2] to generate public/private key pair, encapsulate and decapsulate the shared secret for all the related post-quantum KEM algorithms. Since the liboqs library is incompatible with the
native Hyperledger Fabric docker image for chaincode execution,
we build a new docker image integrated with liboqs based on Ubuntu 18.04 and use it as the execution environment of our
chaincodes. The versions of docker and docker-compose we use
are 19.03.13 and 1.25.0-rc1. For developers, the configuration
files for the client codes, the docker file to generate the new
docker image and information about how to use the new image
are also available.

1.In ccenv dockerfile, use the Ubuntu18.04 as the docker image environment, download and install liboqs library required for the experiment, install and configure the Go env(go1.15.7.linux-amd64.tar.gz).

2.Build the dockerfile.

   ```javascript
   docker built -t ccenv:latest ./ 
   ```
