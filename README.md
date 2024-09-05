# Avalanche HYPERSDK PROJECT

This project uses HyperSDK to create a custom virtual machine, offering complete control over a custom blockchain. By using HyperSDK, we can tailor the blockchain to meet the specific needs of your startup.

## Description 

- **consts/consts.go**: Contains constants accessible across the hyperVM, defining information about the TokenVM, including its Human-Readable Part (HRP), name, and symbol.

- **registry/registry.go**: Contains the actions performed in the terminal during interaction.

## Steps of Execution

This project runs on WSL (Windows Subsystem for Linux) with GO installed inside WSL.

1. Clone the repository:
    ```bash
    git clone https://github.com/Ms-10182/avax-advance-mod-2.git
    ```

2. Navigate to the project directory:
    ```bash
    cd avax-advance-mod-2
    ```

3. Due to GitHub's file size restrictions, the files are provided in a zip file. Extract the **Avalanche hyperSDK project**.

4. Navigate to the extracted directory:
    ```bash
    cd './Avalanche hyperSDK project/'
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
chainID: 2vCjHv1ws8YirjkcjsaVotLhCeownJDVBhUJgtBpu6j9ucupgf
metadata (can be changed later): GoCoin
continue (y/n): y
✅ txID: 2jce33uBTSa3yKrv7KngEdbwtyN4NBXfhGmx4Xtb6p6nPjtb9w
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
chainID: 2skpAtPgFs5v5v2nzWaZKVrfRVxPXAVyfMQANy6EpFjG8dMQTo
assetID: 2fwV7cjRpH7jmK43BWtUc6uTo5Py6wKXBfdQ4CH6BwRMmEmdDe
metadata: GoCoin supply: 0
recipient: token1rvzhmceq997zntgvravfagsks6w0ryud3rylh4cdvayry0dl97nsjzf3yp
amount: 100
continue (y/n): y
✅ txID: 2hvyq3DSVHMwiWuJXPBy8T9LS2MjiX9Ki8ti625Vofrn7L1Ahi
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
chainID: 2skpAtPgFs5v5v2nzWaZKVrfRVxPXAVyfMQANy6EpFjG8dMQTo
✔ assetID (use TKN for native token): 2fwV7cjRpH7jmK43BWtUc6uTo5Py6wKXBfdQ4CH6BwRMmEmdDe█
uri: http://127.0.0.1:46526/ext/bc/2skpAtPgFs5v5v2nzWaZKVrfRVxPXAVyfMQANy6EpFjG8dMQTo
metadata: GoCoin supply: 100 warp: false
balance: 100 2fwV7cjRpH7jmK43BWtUc6uTo5Py6wKXBfdQ4CH6BwRMmEmdDe
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
