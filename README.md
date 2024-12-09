# Zenchain Validator Node (Self host)


![Banner](https://github.com/SKaaalper/zenchain-validator-node/blob/main/zenchain.jpg)


### **Introducing the first decentralized, EVM-compatible Bitcoin Layer 1, designed to enhance secure and seamless cross-chain interactions between Bitcoin and Ethereum. This innovation is a key part of the [Unizen](https://x.com/unizen_io) ecosystem, enabling a new era of interoperability and scalability for decentralized finance.**


### **Zenchain has already secured [$200 million in funding](https://cryptorank.io/ico/unizen#funding-rounds), underscoring strong confidence and support from the blockchain community and investors.**


## Zenchain Official Account
- [Twitter](https://x.com/zen_chain)
- [Discord](https://discord.com/invite/zenchain)
- [Website](https://www.zenchain.io/)
- [Telegram](https://t.me/ZenchainAnnouncements)


## **Need a VPS?**

- You can purchase one from PQ Hosting using cryptocurrency: [https://pq.hosting/](https://pq.hosting/?from=622403&lang=en)
- If you prefer paying via PayMaya, you can use Contabo: [https://contabo.com/en/vps/](https://contabo.com/en/vps/)


## **Here's how to participate as a self-node validator**

1. Join the waitlist first to gain access to the faucet, Visit: [https://www.zenchain.io/waitlist](https://www.zenchain.io/waitlist)

2. After you register for the waitlist, claim the faucet here: [https://faucet.zenchain.io/](https://faucet.zenchain.io/)

## Installation:

1. Update System Packages:
```
sudo su
apt update
sudo apt install -y curl wget tar jq git
```

2.  Install Docker (if not installed):
```
apt install docker.io -y
```

3. Create a Folder and Set Permissions:
```
mkdir -p "$HOME/chain-data"
chmod -R 777 "$HOME/chain-data"
```

4. Run the Node (Temporary Setup - For Session Keys):

- Replace `NamaValidatorAnda` with your desired `validator name`.
```
docker run \
    -d \
    --name zenchain \
    -p 9944:9944 \
    -v "$HOME/chain-data:/chain-data" \
    ghcr.io/zenchain-protocol/zenchain-testnet:latest \
    ./usr/bin/zenchain-node \
    --base-path=/chain-data \
    --rpc-cors=all \
    --rpc-methods=unsafe \
    --unsafe-rpc-external \
    --validator \
    --name=NamaValidatorAnda \
    --bootnodes=/dns4/node-7242611732906999808-0.p2p.onfinality.io/tcp/26266/p2p/12D3KooWLAH3GejHmmchsvJpwDYkvacrBeAQbJrip5oZSymx5yrE \
    --chain=zenchain_testnet
```

5. Run this command to retrieve the session key:
```
curl -H "Content-Type: application/json" -d '{"id":1, "jsonrpc":"2.0", "method": "author_rotateKeys", "params":[]}' http://localhost:9944
```

- The session key will appear as a hexadecimal string starting with `0x`. Remove the `0x` prefix for the next steps.

6. Bind the Session Key to Your Wallet:

### Add Zenchain RPC tok OKX wallet:

- **Network name** : `Zenchain Testnet`
- **RPC URL**: `https://zenchain-testnet.api.onfinality.io/public`
- **Chain ID**: `8408`
- **SYMBOL**: `ZCX`
- **Block Explorer**: `https://zentrace.io/`

**In OKX Wallet, make sure it’s set to the Zenchain Testnet network. Initiate a transaction with these details:**

- **To**: `0x0000000000000000000000000000000000000802`

- **Amount**: `0`

- **Input Data**: `0xf1ec919c00000000000000000000000000000000000000000000000000000000000000200000000000000000000000000000000000000000000000000000000000000060` + `session key without 0x` go to your VPS and copy the `session key`

7. Stop and Remove Docker Container:
```
docker rm -f zenchain
```

- Now that the session key is bound, run the node with the final setup command. Replace `NamaValidatorAnda` with your `validator name`.

```
docker run \
    -d \
    --name zenchain \
    -p 9944:9944 \
    -v "$HOME/chain-data:/chain-data" \
    ghcr.io/zenchain-protocol/zenchain-testnet:latest \
    ./usr/bin/zenchain-node \
    --base-path=/chain-data \
    --validator \
    --name="NamaValidatorAnda" \
    --bootnodes=/dns4/node-7242611732906999808-0.p2p.onfinality.io/tcp/26266/p2p/12D3KooWLAH3GejHmmchsvJpwDYkvacrBeAQbJrip5oZSymx5yrE \
    --chain=zenchain_testnet
```

8. Check Docker Logs `(Monitor the Node)`:
```
docker logs -f zenchain
```

9. Now, go to Validator Dashboard: [https://node.zenchain.io/#/staking](https://node.zenchain.io/#/staking)

- Cick `Stake` > Click `To Your Account` > Click `Become a Validator` > Input any amount you want to stake > Click `Start Staking` and Done!

10. Verify Node Status:
- After about 1–2 hours, check if your node is visible on the Zenchain validator list via the staking dashboard.

And, That's it! 🚀


