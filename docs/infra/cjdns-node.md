# Setup a Cjdns Node
This guide will help you set up a cjdns node on a server.

## Requirements
A server running debian based Linux (preferably Ubuntu 22.04) with docker installed

## Steps

* Create a data directory where the server configuration will be stored.

    ```
    mkdir vpn_data
    ```

* Get the latest docker image

    ```
    docker pull pkteer/pkt-server
    ```

* Configure the server by running the following command:

    ```
    docker run -it --rm -v $(pwd)/vpn_data:/data pkteer/pkt-server /configure.sh --novpn
    ```

The configure process will create: `* a cjdroute.conf at data/cjdroute.conf * PKT wallet at data/pktwallet/pkt/wallet.db * store the wallet's seed phrase at data/pktwallet/pkt/seed.txt`
configure.sh can take the following flags: `* --no-vpn:` To configure the server without setting up the VPN server `* --with-pktd:` To configure the server with a local PKT daemon `* --pktd-passwd= :` To set a password for the PKT daemon

Alternatively you can edit the __config.json__ file manually.


!!! warning "NOTE" 
    Make sure to safely store your seed phrase in order to be able to import your wallet on your computer. And delete the __seed.txt__ file after.

* Run the server by running the following commands:
    ```
    ./vpn_data/start.sh
    ```

    This will start the server and may expose the following ports: 
    `* cjdns port set from cjdroute.conf * cjdns admin rpc port set from cjdroute.conf (default 11234) * 8099 for anodevpn server * 5201 for iperf3 * 64764` for pktd