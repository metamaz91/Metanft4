# Metanft4
Cooking new version
Skandha

A modular, developer-friendly Typescript Bundler for Ethereum EIP-4337 Account Abstraction

Warning! This repo/software is under active development
⚙️ How to run (from Source code)
Run with one-liner:

curl -fsSL https://skandha.run | bash
or follow steps below:

install all dependencies by running yarn
build yarn build && yarn bootstrap
cp config.json.default config.json
edit config.json
(optional) run local geth-node from test/geth-dev
run ./skandha
Skandha will run for all chains available in config.json
Networks will be available at http://localhost:14337/{chainId}/ (e.g. for dev http://localhost:14337/1337/)
🐳 How to run (a Docker image)
cp config.json.default config.json
edit config.json
docker build -t etherspot/skandha .
docker run --mount type=bind,source="$(pwd)"/config.json,target=/usr/app/config.json,readonly -dp 14337:14337 etherspot/skandha start
📜 Additional features
 Unsafe mode - bypass opcode & stake validation
 Redirect RPC - Redirect ETH rpc calls to the underlying execution client. This is needed if you use UserOp.js
⚡️ CLI Options
--unsafeMode - enables unsafeMode
--redirectRpc - enables redirecting eth rpc calls
🔑 Relayer Configuration
config.json
{
  "networks": {
    "dev": { # network Id (check packages/types/src/networks/networks.ts)
      "entryPoints": [ # supported entry points
        "0x5FF137D4b0FDCD49DcA30c7CF57E578a026d2789"
      ],
      "relayer": "0xprivateKey", # relayer private key, can access from here or via environment variables (SKANDHA_MUMBAI_RELAYER | SKANDHA_DEV_RELAYER | etc.)
      "beneficiary": "0xf39Fd6e51aad88F6F4ce6aB8827279cffFb92266", # fee collector, avaiable via env var (SKANDHA_MUMBAI_BENEFICIARY | etc)
      "rpcEndpoint": "http://localhost:8545", # rpc provider, also available via env variable (SKANDHA_MUMBAI_RPC | etc)
      "minInclusionDenominator": 10, # optional, see EIP-4337
      "throttlingSlack": 10, # optional, see EIP-4337
      "banSlack": 10 # optional, see EIP-4337
      "minSignerBalance": 1, # optional, default is 0.1 ETH. If the relayer's balance drops lower than this, it will be selected as a fee collector
      "multicall": "0x", # optional, address of multicall3 contract, default is 0xcA11bde05977b3631167028862bE2a173976CA11 (see https://github.com/mds1/multicall#multicall3-contract-addresses)
    }
  }
}
Enjoy your night
