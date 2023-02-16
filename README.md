# Buidl the contract

cargo concordium build --out dist/fungible/module.wasm.v1 --schema-out dist/fungible/schema.bin

# Deploy the contract

concordium-client module deploy dist/fungible/module.wasm.v1 --sender YOUR-ACCOUNT --name YOUR-CONTRACT-NAME --grpc-port 10000 --grpc-ip node.testnet.concordium.com

# Initialize the contract

concordium-client contract init MODULE-HASH --sender YOUR-ACCOUNT --energy 30000 --contract fungible-cis2 --grpc-port 10000 --grpc-ip node.testnet.concordium.com

# Mint Fungible Tokens

concordium-client contract update YOUR-CONTRACT-INSTANCE --entrypoint mint --parameter-json token-artifacts/mint-params.json --schema dist/fungible/schema.bin --sender YOUR-ACCOUNT --energy 6000 --grpc-port 10000 --grpc-ip node.testnet.concordium.com

# View Contract State

concordium-client contract invoke YOUR-CONTRACT-INSTANCE --entrypoint view --schema dist/fungible/schema.bin --grpc-port 10000 --grpc-ip node.testnet.concordium.com

# Check Metadata

concordium-client contract invoke YOUR-INDEX --entrypoint tokenMetadata --parameter-json token-artifacts/ids.json --schema dist/fungible/schema.bin --grpc-port 10001

# Transfer

concordium-client contract update YOUR-INDEX --entrypoint transfer --parameter-json token-artifacts/transfer.json --schema dist/fungible/schema.bin --sender YOUR-ACCOUNT --energy 6000 --grpc-port 10000 --grpc-ip node.testnet.concordium.com

# Burn

concordium-client contract update YOUR-INDEX --entrypoint burn --parameter-json token-artifacts/burn.json --schema dist/fungible/schema.bin --sender YOUR-ACCOUNT --energy 6000 --grpc-port 10000 --grpc-ip node.testnet.concordium.com
