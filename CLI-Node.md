# CLI Node Run Full Guide (PC+Mobile)

### Offical Docs by Pipe Network - https://docs.shelby.xyz/tools/cli

----

## 🧰 Prerequisites
	
1. Go to Github https://github.com/new
2. Make New Repository name (e.g. `shelby-node`)
3. Click the green `Code` button
4. Select → `Open with Codespaces` → `+ New codespace`
5. Wait for the environment to fully load

----

1 Dependencies for WINDOWS & LINUX & VPS
```
sudo apt-get update && sudo apt-get upgrade -y
```
```
sudo apt install curl iptables build-essential git wget lz4 jq make gcc nano automake autoconf tmux htop nvme-cli libgbm1 pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip libleveldb-dev  -y
```
```
sudo apt install -y libssl-dev ca-certificates
```

2 Install Node.js & Git
```
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
sudo apt install -y nodejs git
```
```
node -v
npm -v
git --version
```

3 Install Shelby CLI
```
npm i -g @shelby-protocol/cli
```
```
shelby --version
```

4 Get Your API Key

1. Open **https://geomi.dev**
2. Click **Sign Up** and create an account
3. On the overview page, click **"API Resource"**
4. Fill in:
   - **Network:** `Shelbynet`
   - **Resource Name:** `my-shelby`
   - **Usage Description:** `storage`
5. Click **Submit**
6. **Copy your API key** (starts with `aptoslabs_...`)

5 Initialize Shelby
```
shelby init
```

When prompted:

| Prompt | Action |
|--------|--------|
| API Key | Paste your API key from Step 4 |
| Private Key | Press **Enter** to generate new (or paste existing) |
| Other prompts | Press **Enter** to accept defaults |

How To Get Your Shelby Wallet Private Key
```
shelby account list
```
```
nano ~/.shelby/config.yaml
```

6 Get Free Tokens

You need **APT** (gas fees) and **ShelbyUSD** (storage fees).

```
shelby faucet --no-open
```

This displays a faucet URL. Copy it and open in your browser.

On the faucet page:
1. Your address is pre-filled
2. Click **Fund** to get APT tokens
3. Click **Fund** again for ShelbyUSD tokens

7 Check Your Balance
```
shelby account balance
```

You should see both **APT** and **ShelbyUSD** with balances > 0.

8 Create and Upload a File
```
echo "YOUR OG DAD!" > eba.txt
```
```
shelby upload eba.txt myfile.txt -e "in 7 days" --assume-yes
```

9 Verify Upload
```
shelby account blobs
```

You should see `myfile.txt` in the list.

10 Download the File
```
shelby download myfile.txt downloaded.txt
```

Check it worked:

```
cat downloaded.txt
```

Output: `Hello Shelby Babes!`

---

### 🔶For Next Day Run This Command

1 Resume Codespace

1. Go to your GitHub repository
2. Click **Code → Codespaces**
3. Click **Resume**

Wait until terminal loads.

2 Check Shelby CLI
```
shelby --version
```

If version shows → good ✅
(No need to reinstall)

4 Check Balance
```
shelby account balance
```

If ShelbyUSD low → run:

```
shelby faucet --no-open
```

Open faucet link in browser and fund again.

5 Create New Daily File
```
echo "Shelby Daily Activity" > daily.txt
```

6 Upload With Unique Name

Very important → unique name daily

```
shelby upload daily.txt daily-$(date +%F-%H-%M-%S).txt -e "in 7 days" --assume-yes
```

Example file name:
```
daily-2026-02-15.txt
```

7 Verify Upload
```
shelby account blobs
```

You should see `daily-2026-02-15.txt` in the list.

8 Download the File
```
shelby download daily-2026-02-15.txt downloaded.txt
```

Check it worked:

```
cat downloaded.txt
```

Output: `Shelby Daily Activity`
