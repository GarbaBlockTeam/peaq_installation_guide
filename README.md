# peaq_installation_guide
```markdown
# Krest Node Setup and Runtime Upgrade (v0.0.6)

This guide will help you set up and upgrade a Krest node to the latest version. The v0.0.6 release updates dependent libraries to enhance network features and stability, unifying the RPC and WS ports for improved performance.

## Notice for Existing Node Operators

- The krest runtime upgrade (v0.0.6) includes several crucial improvements.
- **Key changes:** Unification of RPC and WS ports. Ensure you update your binary/docker configurations to ensure a seamless experience.
- **Action required:** Update your nodes for optimal performance, especially for EVM functionality.

## Upgrade Steps

1. **Stop the Docker container**  
   Ensure to keep the Docker volume intact to avoid data loss.

2. **Update Docker image**  
   Pull the updated Docker image from the link provided below.

3. **Remove Unsafe Flags (if applicable)**  
   If you've already generated session keys, ensure to remove the following flags from your node configuration:
   - `--unsafe-rpc-external`
   - `--rpc-methods=unsafe`

4. **Restart with Updated Image**  
   Run your updated Docker image with the following command:

   ```bash
   sudo docker run -d -v krest-storage:/chain-data -p 9944:9944 -p 9933:9933 peaq/parachain:krest-v0.0.7 \
   --collator \
   --parachain-id 2241 \
   --chain ./node/src/chain-specs/krest-raw.json \
   --base-path chain-data \
   --port 30333 \
   --rpc-port 9944 \
   --rpc-methods=unsafe \
   --unsafe-rpc-external \
   --rpc-cors=all \
   --execution=wasm \
   --out-peers 50 \
   --in-peers 50 \
   -- \
   --execution wasm \
   --chain ./node/src/chain-specs/kusama.json \
   --port 30343 \
   --sync warp \
   --rpc-port 9977
   ```

