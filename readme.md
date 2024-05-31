# Fuel Node Kurulumu ve Yapılandırması

Bu depo, yerel bir Fuel node'unu Testnet'e bağlı olarak çalıştırmak için gerekli olan tüm adımları ve yapılandırma dosyalarını içermektedir.

## Kurulum

### Fuel Araç Zincirinin Yüklenmesi

Fuel araç zincirini yüklemek için aşağıdaki komutu çalıştırın:

```sh
curl https://install.fuel.network | sh
```

**Testnet Araç Zincirinin Yüklenmesi**
Testnet araç zincirini yüklemek için aşağıdaki komutları çalıştırın:
```sh
fuelup toolchain install testnet
fuelup default testnet
```

**Sepolia API Anahtarı Alımı**
Sepolia (Ethereum Testnet) ağı için bir API anahtarı alın. [Infura](https://www.infura.io/) veya [Alchemy](https://www.alchemy.com/) kullanabilirsiniz:

Infura: https://sepolia.infura.io/v3/{YOUR_API_KEY}

Alchemy: https://eth-sepolia.g.alchemy.com/v2/{YOUR_API_KEY}


**P2P Anahtarı Oluşturma**
Yeni bir P2P anahtarı oluşturmak için aşağıdaki komutu çalıştırın:
```sh
fuel-core-keygen new --key-type peering
```
**Anahtarınızı güvenli bir yerde saklayın.**

**Yapılandırma Dosyaları**
**Gerekli yapılandırma dosyaları bu depoda sağlanmıştır:**

*[chain_config.json](https://github.com/eftay17/fuel_network/blob/main/chain_config.json)

*[metadata.json](https://github.com/eftay17/fuel_network/blob/main/metadata.json)

*[state_config.json](https://github.com/eftay17/fuel_network/blob/main/state_config.json)

*[Buradan indirip sunucunuza atın](https://github.com/FuelLabs/fuel-core/raw/9fddeccb4d112c148f6793bc3d21131a13778a25/bin/fuel-core/chainspec/testnet/state_transition_bytecode.wasm)

**Yerel Node'un Çalıştırılması**
Yerel node'u çalıştırmak için aşağıdaki komutu kullanın:
```sh
fuel-core run \
--service-name {ANY_SERVICE_NAME} \
--keypair {P2P_SECRET} \
--relayer {ETH_RPC_ENDPOINT} \
--ip 0.0.0.0 --port 4000 --peering-port 30333 \
--db-path  ~/.testnet \
--snapshot ./path/to/chain_config_folder \
--utxo-validation --poa-instant false --enable-p2p \
--min-gas-price 1 --max-block-size 18874368 --max-transmit-size 18874368 \
--reserved-nodes /dns4/p2p-devnet.fuel.network/tcp/30333/p2p/16Uiu2HAm6pmJUedRFjennk4A8yWL6zCApHCuykzRRroqMjjxZ8o6,/dns4/p2p-devnet.fuel.network/tcp/30334/p2p/16Uiu2HAm8dBwTRzqazCMqQDdR8thMa7BKiW4ep2B4DoQQp6Qhyfd \
--sync-header-batch-size 100 \
--enable-relayer \
--relayer-v2-listening-contracts 0x01855B78C1f8868DE70e84507ec735983bf262dA \
--relayer-da-deploy-height 5827607 \
--relayer-log-page-size 2000
```
**Bağlanma**
Yerel node'a bir tarayıcı cüzdanı ile bağlanmak için aşağıdaki ağı kullanın:
```sh
http://0.0.0.0:4000/graphql
```
