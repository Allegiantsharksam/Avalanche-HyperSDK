# Avalanche HYPERSDK PROJECT

This project uses HyperSDK to create a custom virtual machine, offering complete control over a custom blockchain. By using HyperSDK, we can tailor the blockchain to meet the specific needs of your startup.

## Description 

- **consts/consts.go**: Contains constants accessible across the hyperVM, defining information about the TokenVM, including its Human-Readable Part (HRP), name, and symbol.

- **registry/registry.go**: Contains the actions performed in the terminal during interaction.

## Steps of Execution

This project runs on WSL (Windows Subsystem for Linux) with GO installed inside WSL.

1. Clone the repository:
    ```bash
    git clone https://github.com/Allegiantsharksam/Avalanche-HyperSDK.git
    ```

2. Navigate to the project directory:
    ```bash
    cd Avalanche-HyperSDK
    ```

3. Due to GitHub's file size restrictions, the files are provided in a zip file. Extract the **Avalanche hyperSDK project**.

4. Navigate to the extracted directory:
    ```bash
    cd './Avalanche-HyperSDK/'
    ```

5. Start the machine with 1 subnet:
    ```bash
    MODE="run-single" ./scripts/run.sh
    ```
    For 2 subnets, run:
    ```bash
    ./scripts/run.sh
    ```
    The output will be:
    ```javascript
    Ran 4 of 4 Specs in 81.284 seconds
    PASS
    cluster is ready!
    avalanche-network-runner is running in the background... 

    use the following command to terminate:

    killall avalanche-network-runner
    ```

6. Build the CLI:
    ```bash
    ./scripts/build.sh
    ```
    The output will be:
    ```javascript
    /scripts/build.sh
    Building tokenvm in ./build/tHBYNu8ikqo4MWMHehC9iKB9mR5tB3DWzbkYmTfe9buWQ5GZ8
    Building token-cli in ./build/token-cli
    ```
    
    This command will place the compiled CLI in `./build/token-cli`.
    **Note**: The default address is `token1rvzhmceq997zntgvravfagsks6w0ryud3rylh4cdvayry0dl97nsjzf3yp`.

7. Add the chains and the default key to the token-cli:
    ```bash
    ./build/token-cli key import demo.pk
    ./build/token-cli chain import-anr
    ```

## Creation and Minting Process

### Step 1: Asset Creation

Create an asset:
```bash
./build/token-cli action create-asset
```
Enter the metadata (e.g., GoCoin) and confirm. The output will be:
```javascript
database: .token-cli
address: token1rvzhmceq997zntgvravfagsks6w0ryud3rylh4cdvayry0dl97nsjzf3yp
chainID: 2EMjCLBNVFD9aJRRkPcFbxTpre3kNAqjPrK9s8oRBPMq5QfzQT
metadata (can be changed later): GoCoin
continue (y/n): y
✅ txID: 27Ps5AFs7FQmLkbMC433Lu368tT9ZNPVJ3dWdwEubwqBJ3sGZT
```
**Note**: `txID` is the assetID of your new asset.

### Step 2: Minting the Asset

Mint the created asset:
```bash
./build/token-cli action mint-asset
```
Enter the assetID, recipient, amount, and confirm. The output will be:
```javascript
database: .token-cli
address: token1rvzhmceq997zntgvravfagsks6w0ryud3rylh4cdvayry0dl97nsjzf3yp
chainID: 2EMjCLBNVFD9aJRRkPcFbxTpre3kNAqjPrK9s8oRBPMq5QfzQT
in assetID (use TKN for native token): TKN
out assetID (use TKN for native token): 2iiv7Ca55gxwdQHszva1tY4b8A86q8ES3Yqd3vuvCTiePG8Uoy
✔ out assetID (use TKN for native token): 2iiv7Ca55gxwdQHszva1tY4b8A86q8ES3Yqd3vuvCTiePG8Uoy█
metadata: cu supply: 100000 warp: false
balance: 100000 2iiv7Ca55gxwdQHszva1tY4b8A86q8ES3Yqd3vuvCTiePG8Uoy
out tick: 1000
✔ continue (y/n): Y█
✅ txID: ubpeJfXnqkcb7jDHsNvEU4SabezE9XwofF8WwEmHF6hTv1zVS
```

### Step 3: Check Balance

Check the balance:
```bash
./build/token-cli key balance
```
Enter the assetID of the token. The output will be:
```javascript
database: .token-cli
address: token1rvzhmceq997zntgvravfagsks6w0ryud3rylh4cdvayry0dl97nsjzf3yp
chainID: 2EMjCLBNVFD9aJRRkPcFbxTpre3kNAqjPrK9s8oRBPMq5QfzQT
in assetID (use TKN for native token): TKN
balance: 999.999998638 TKN
out assetID (use TKN for native token): 2iiv7Ca55gxwdQHszva1tY4b8A86q8ES3Yqd3vuvCTiePG8Uoy
metadata: cu supply: 100000 warp: false
available orders: 1
0) Rate(in/out): 1000000.0000 InTick: 1.000000000 TKN OutTick: 1000 2iiv7Ca55gxwdQHszva1tY4b8A86q8ES3Yqd3vuvCTiePG8Uoy Remaining: 10000 2iiv7Ca55gxwdQHszva1
select order: 0
value (must be multiple of in tick): 1
in: 1.000000000 TKN out: 1000 2iiv7Ca55gxwdQHszva1tY4b8A86q8ES3Yqd3vuvCTiePG8Uoy
continue (y/n): y
✅ txID: 27Ps5AFs7FQmLkbMC433Lu368tT9ZNPVJ3dWdwEubwqBJ3sGZT
```

### Additional: Watch the Blockchain

Watch the blockchain:
```bash
./build/token-cli chain watch
```
From the listed chainID, enter the desired index of the chainID to start live watching of the blockchain.

### Closing

Close the blockchain:
```bash
killall avalanche-network-runner
```

**Note:** Couldn't add the test e2e file because of its size.
