
# EigenLayer Node Operator Guide

## Introduction
Welcome to the EigenLayer Node Operator Guide. This step-by-step tutorial will assist you in setting up and running a node on EigenLayer.

### Connect with Me
- [Twitter](https://twitter.com/Moeenxyz)
- [Lens Profile](https://lenster.xyz/u/moeen)

If you find this guide helpful, consider delegating to me:
- [Moeen's Operator Profile](https://goerli.eigenlayer.xyz/operator/0xe3c694453d69caea4edcbb0bb8d24accc6932565)

## Setting Up Your Node

### Choosing a VPS
Get a VPS, for Operators there is no minumum config mentioned but if you want to do AVS, for optimal performance, following minimum specifications:
- vCPUs: 16
- Memory: 32GB
- Storage: 3.6T (High-performance SSD)
- Network Utilization: 24 Mbps download, 120 Mbps upload, Peak 1 Gbps
- Suggested EC2 Equivalent: m5.4xlarge

I personally use Hetzner. Here's a referral link that provides €20 credit: [Hetzner Cloud](https://hetzner.cloud/?ref=p7amgYr2ILM7).

### Operating System Requirements
- Preferred OS: Ubuntu 22.04
- Recommended CPU: AMD

## Installation Steps

### Update Ubuntu
First, update your Linux system:

```shell
sudo apt update
sudo apt upgrade
```

### Installing Docker and Docker Compose
Install Docker and Docker Compose using the following commands:

```shell
# Adding Docker's GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

# Adding Docker repository:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

Verify Docker installation:

```shell
sudo docker run hello-world
```

Next, install Docker Compose:

```shell
sudo apt install docker-compose
sudo curl -L https://github.com/docker/compose/releases/download/v2.16.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker compose version
```

You should see: Docker Compose version vX.XX.X

### Installing EigenLayer CLI
Download and install the EigenLayer CLI:

```shell
curl -L https://github.com/NethermindEth/eigenlayer/releases/download/v0.4.3/eigenlayer-linux-amd64 --output eigenlayer
chmod +x ./eigenlayer
```

### Key Management
Generate your ECDSA and BLS keys using the EigenLayer CLI. Replace `[keyname]` with your preferred key name.

```shell
./eigenlayer operator keys create --key-type ecdsa [keyname]
./eigenlayer operator keys create --key-type bls [keyname]
```

During this process, the CLI will prompt you to create a password for encrypting your private keys. Ensure this password is secure and stored safely, as it will be needed to access your keys. The output will provide several key details, including the ECDSA Private Key (Hex), Key location, Public Key hex, Operator Ethereum Address, BLS Private Key, BLS Public Key, and their respective locations. It’s crucial to securely save this information.

For key importation guidelines, refer to the [EigenLayer Documentation](https://docs.eigenlayer.xyz/operator-guides/operator-installation#import-keys).

### Creating Operator Metadata
Prepare your operator metadata and save it as `metadata.json`, upload it, and get the link. Ensure your logo is in PNG format and that the file is hosted publicly. Example metadata:

```json
{
  "name": "Some operator",
  "website": "https://www.example.com",
  "description": "I operate on some data",
  "logo": "https://www.example.com/logo.png",
  "twitter": "https://x.com/example"
}
```

### Configuring Your Operator
Create and configure your operator settings:

```shell
./eigenlayer operator config create
```

Fill in the details as prompted. Example entries:
```
Would you like to populate the operator config file? Yes
Enter your operator address: [your operator address from previous steps]
Do you want to gate stakers approval? No
Enter your earnings address (default to your operator address): [your wallet address for earnings]
Enter your ETH rpc url: [e.g., https://rpc.ankr.com/eth_goerli]
Enter your ecdsa key path: [your ecdsa Key location]
Enter your bls key path: [your bls Key location]
Select your network: goerli
```

### Finalizing Operator Setup
Edit the `operator.yaml` file to include necessary data:

```shell
nano operator.yaml
```

Add the following information, updating the `metadata_url` and smart contract addresses as needed. Refer to the [EigenLayer Operator Guide](https://docs.eigenlayer.xyz/operator-guides/operator-installation#goerli-smart-contract-addresses) for the latest addresses.

```yaml
metadata_url: link to your metadata.json
el_slasher_address: 0xD11d60b669Ecf7bE10329726043B3ac07B380C22
bls_public_key_compendium_address: 0xc81d3963087Fe09316cd1E032457989C7aC91b19
```

Transfer GoerliETH to your operator address for fees, then execute:

```shell
./eigenlayer operator register operator-config.yaml
```

Verify your operator status:

```shell
./eigenlayer operator status operator.yaml
```

If the status shows “Operator is registered,” your setup is complete. Check your operator listing at [EigenLayer Operator Page](https://goerli.eigenlayer.xyz/operator/).

### Support My Work
If you found this guide useful, consider delegating to me:
- [Delegate to Moeen](https://goerli.eigenlayer.xyz/operator/0xe3c694453d69caea4edcbb0bb8d24accc6932565)


