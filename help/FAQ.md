## Contents

### General mining
* [How do I start mining?](#how-do-i-start-mining)  
* [What should I mine?](#what-should-i-mine)  
* [I have been mining for hours now, but there is nothing in my wallet, is that normal?](#i-have-been-mining-for-hours-now-but-there-is-nothing-in-my-wallet-is-that-normal)  
* [Windows says my GPU usage is very low, is this normal?](#windows-says-my-gpu-usage-is-very-low-is-this-normal)  

### Configuration / setup
* [Antivirus alerts (miner shows T-Rex.exe not found error in red)](#antivirus-alerts-miner-shows-t-rexexe-not-found-error-in-red)  
* [How do I verify miner authenticity?](#how-do-i-verify-miner-authenticity)  
* [How do DEV Fees work when single-coin mining?](#how-do-dev-fees-work-when-single-coin-mining)  
* [How do DEV Fees work when dual-mining?](#how-do-dev-fees-work-when-dual-mining)  
* [What CUDA version should I use?](#what-cuda-version-should-i-use)  
* [Will validating shares influence my hashrate?](#will-validating-shares-influence-my-hashrate)  
* [How do I pause a rig/miner?](#how-do-i-pause-a-rigminer)  
* [How do I set extra parameters in HiveOS?](#how-do-i-set-extra-parameters-in-hiveos)  
* [How do I add backup pools?](#how-do-i-add-backup-pools)  
* [How do I run T-Rex as an administrator?](#how-do-i-run-t-rex-as-an-administrator)  

### LHR
* [What is LHR?](#what-is-lhr)  
* [What cards are LHR?](#what-cards-are-lhr)  
* [What is LHR unlock dual mining mode?](#what-is-lhr-unlock-dual-mining-mode)  
* [Why does my GPU keep hitting LHR locks?](#why-does-my-gpu-keep-hitting-lhr-locks)  

### User interface
* [What are the red numbers behind the "R:"?](#what-are-the-red-numbers-behind-the-r)  
* [What does the red (!) mean?](#what-does-the-red--mean)  
* [What do the temperature numbers in T-Rex mean?](#what-do-the-temperature-numbers-in-t-rex-mean)  
* [Why can't I see memory temperatures in T-Rex?](#why-cant-i-see-memory-temperatures-in-t-rex)  

### WebUI / API
* [How do I create an API Key?](#how-do-i-create-an-api-key)  
* [How do I use an API Key once I've created it?](#how-do-i-use-an-api-key-once-ive-created-it)  
* [Why can't I save settings in the WebUI?](#why-cant-i-save-settings-in-the-webui)  
* [Where can I see WebUI for my miner?](#where-can-i-see-webui-for-my-miner)  
* [How do I see the T-Rex WebUI from another computer or phone on my local network?](#how-do-i-see-the-t-rex-webui-from-another-computer-or-phone-on-my-local-network)  
* [What do the lines on the graph mean?](#what-do-the-lines-on-the-graph-mean)  

### Tuning
* [Where do I find the best OC (overclock) settings for my GPU?](#where-do-i-find-the-best-oc-overclock-settings-for-my-gpu)  
* [Why does my hashrate go lower when I keep increasing my --mclock value?](#why-does-my-hashrate-go-lower-when-i-keep-increasing-my---mclock-value)  
* [What is the difference between --lock-cclock and --cclock?](#what-is-the-difference-between---lock-cclock-and---cclock)  
* [What intensity or kernel should I use?](#what-intensity-or-kernel-should-i-use)  
* [How do I run a benchmark?](#how-do-i-run-a-benchmark)  
* [How does memtweak work?](#how-does-memtweak-work)  

### Miscellaneous errors / issues
* [High CPU usage](#high-cpu-usage)  
* [What are error codes 15 and 999?](#what-are-error-codes-15-and-999)  
* [I'm getting a "code -6"](#im-getting-a-code--6)  
* [What is the "instance wasn't validated" error?](#what-is-the-instance-wasnt-validated-error)  
* [T-Rex reports very high VRAM temps, is this safe?](#t-rex-reports-very-high-vram-temps-is-this-safe)  
* [I'm getting a "No connection" error, but my network connection is fine](#im-getting-a-no-connection-error-but-my-network-connection-is-fine)  
* [Why does --autoupdate not work?](#why-does---autoupdate-not-work)  
* [Why are some of my config.json settings not working?](#why-are-some-of-my-configjson-settings-not-working)  



## How do I start mining?
Before you can mine, you need a crypto wallet. [MetaMask](https://metamask.io/) is an easy to setup/use wallet that works in your browser and on your phone.

If you would prefer an application based wallet, you can use a wallet like [Exodus](https://www.exodus.com/) or [Atomic](https://atomicwallet.io/) which have similar ease of use like Metamask, but allow for a larger variety of coins.

The next thing you will need is a pool. There are several example `*.bat`/`*.sh` files in your T-Rex folder that connect to reputable mining pools.

The simplest way to get started is to edit one of the ethereum `*.bat`/`*.sh` files in the T-Rex folder and replace the wallet address in there with the receive address from your wallet for the currency you are mining. Then, save and run the `*.bat`/`*.sh` file to start T-Rex.

## What should I mine?
Generally speaking, you should mine the most profitable coin(s) available to you at the time. Visit [WhatToMine](https://www.whattomine.com/) and plug in your numbers to see what makes sense for you. The default numbers they provide for different GPUs are a good indicator, but your results may differ.

## I have been mining for hours now, but there is nothing in my wallet, is that normal?
Yes, that is normal. Depending on your hashrate, it will take you a few days or even weeks before you hit the minimum payout amount and the pool sends it to your wallet. 

Typical minimum payout threshold values on most ETH pools is .1 ETH. Some pools like [Ethermine](https://ethermine.org) have lower minimums, but the payout is on a different layer than mainline ethereum, so there's more work for you to do to get your profits.

More pools are allowing the user to change their minimum payout amount now. For example [Flexpool](https://www.flexpool.io/) allows the user to change this once you verify the public IP of one of your miners [Screenshot](https://i.imgur.com/iogZl1b.png).

## Windows says my GPU usage is very low, is this normal?
Yes, T-Rex uses CUDA to work with your GPU so Windows task manager doesn't properly report usage. [To enable](https://i.imgur.com/4wtmfmK.png)
  
If you can't find CUDA as an option in the drop down menu you need to disable "Hardware-accelerated GPU Scheduling" in your Windows settings. To disable it, go to Start > Settings > Display > Graphics Settings, and turn it off.

## Antivirus alerts (miner shows T-Rex.exe not found error in red)
**Always verify authenticity of your download!** (see next question in the FAQ)
  
In order to protect the miner from reverse engineering attacks, the binaries are packed using a third-party software which mangles the original machine code. As a result, some antivirus engines may detect certain signatures (false positives) within the executable that are similar to those that real viruses have. 
  
Binaries which are taken from the official site https://trex-miner.com/ and the official GitHub https://github.com/trexminer/T-Rex are completely safe. 
  
In any case, it is advisable not to use any cryptocurrency miners on the computers where you store your sensitive data such as wallets, passwords, etc.

## How do I verify miner authenticity?
After you've downloaded the miner archive from the links in releases, it's advisable to verify that its checksum matches the one listed in the release message.

**Windows Powershell:**
```Get-FileHash <PATH_TO_TREX.zip> -Algorithm SHA256 | Format-List```

**Windows CMD:**
```certutil -hashfile <PATH_TO_TREX.zip> SHA256```

**Windows 7-Zip:**
Right click the downloaded zip file, click on "CRC SHA", then select "SHA-256" to get the checksum of the file

**Linux:**
```sha256sum <PATH_TO_TREX.tar.gz>```

## How do DEV Fees work when single-coin mining?
The miner automatically mines to the developers wallet for X/100 minutes, depending on what the fee is. 
Currently, the dev fee for ETH is 1% (2% for Octopus, Autolykos2), so the miner mines for you 99 out of 100 minutes, and for the devs that remaining minute.

## How do DEV Fees work when dual-mining?
Since it's only 30% of ETH, we've set the fees to whatever they are for the second algo, i.e. 2% for dual with ERG and CFX, and 1% for dual with RVN - the miner tells that at start up. 

Initially the idea was to set them to 1% but that opens up a "hack" where you set LHR 10 and pretty much mine ERG or CFX with 1% instead of the usual 2% set for those algorithms. The fees may be reviewed (= decreased) in future releases however.

As for the way they are taken, it's no different to single mode, T-Rex mines the dev fee to the dev wallet during dev fee sessions in dual mode too.

## What CUDA version should I use?
The latest versions of T-Rex include all versions of CUDA, and will automatically select the correct version.

For older versions with multiple downloads, you can choose based on this:
* CUDA 11.x (and 12.x when released) is for 30xx series cards (3060/70/80/90)
* CUDA 10.x (and 11.x) is for 10xx, 16xx and 20xx series cards 

* CUDA is forward-compatible with the next version since CUDA 10.x [See page 7](https://docs.nvidia.com/pdf/CUDA_Compatibility.pdf)

## Will validating shares influence my hashrate?
While it won't influence your hashrate, it can increase the number of stale shares your miner submits, which will impact your profit... especially if you have a slower network connection.
  
If invalid/rejected shares are a concern, you can set the `--validate-shares` option and look at the stats for few days.

If you have no invalid shares then your GPUs are stable and there is no need to use the share validation argument, since it is primarily intended to determine which of your gpus are not stable or working well. 

This feature can be very useful when overclocking, though should be disabled once you verify your overclock is stable.

Note: Some pools incorrectly report invalid shares for issues on their end, so don't chase a red herring if you suspect this and ask about your concern in the Discord for more information.

## How do I pause a rig/miner?
In the WebUI, click the name of the GPU at the bottom of the main page, and then click the pause icon.

## How do I set extra parameters in HiveOS?
HiveOS launches T-Rex using JSON configuration files, so all extra parameters should be set accordingly.
     
A few examples:

* ```--lhr-tune 72,0,30``` becomes ```"lhr-tune": "72,0,30"```
* ```--validate-shares``` becomes ```"validate-shares": true``` Same with all boolean parameters that don't expect values if you specify them in cmd line
* ```-i 25``` becomes ```"intensity": "25"```
       
**Note:** 
There are no short names in JSON, you need to use the full name for one-letter parameters like `-i` (`"intensity"`), `-N` (`"hashrate-avr"`) etc.

## How do I add backup pools?
Just add more pool sections (`-o <pool info>`) to your `*.bat`/`*.sh` file.
Example: ```t-rex -a ethash -o stratum+tcp://us1.ethermine.org:4444 -o stratum+tcp://us2.ethermine.org:4444 -o stratum+tcp://eu1.ethermine.org:4444```
  
Alternatively, you can add them in the WebUI if you are using a config file. [WebUI Wiki](https://github.com/trexminer/T-Rex/wiki/WebUI)

## How do I run T-Rex as an administrator?
There are several methods, but the most common way is to right click the `t-rex.exe` file, select Properties, select the Compatibility tab, and check the Settings box for "Run this program as an administrator", then click OK.

For Linux users you will need to use a priviledged account with ```sudo``` access or the root user. *It is highly discouraged to run any application under the root account; please use sudo if available!*

## What is LHR?
LHR (Lite Hash Rate) is something Nvidia came up with as a way to try to get graphics cards into the hands of gamers instead of miners. It is a built in limit when the card detects that it is mining ETH (or other limited algos) it will limit the hashrate to ~50% of the cards capability. 

T-Rex has found a way to get around this ~50% barrier, and allows mining ETH (and other affected algos) at up to 70% of the cards capability. 

## What cards are LHR?
All RTX cards manufactured after mid-May of 2021 are LHR cards.
The two exceptions to this rule are:
* The RTX 3090 is not LHR
* If you have a Rev.1 3060 with the 470.05 driver on Windows it will not detect as LHR.
You can use GPU-Z from TechPowerUp to see if your card has a LHR GPU, by looking in the GPU field of the main tab of the application.

**LHR SKU Identification:**

3060 models:
* All 3060 models are LHR, no matter their SKU. (See exception above for Rev.1 cards)
           
3070/3080 models
* ASUS – LHR will be marked as version 2 or higher (ex - ROG Strix GeForce RTX™ 3070 V2)
* MSI – LHR will be marked along with the SKU (ex - 3070 GAMING TRIO PLUS 8G LHR) just like ZOTAC
* EVGA – LHR will be marked along with the SKU as "KL" (ex - 8GB GDDR6 08G-P4-3080-KL)
* GIGABYTE - LHR will be marked as version 2 / rev. 2.0 or higher
* ZOTAC - LHR will be marked along with the SKU (ex - RTX 3080 Trinity LHR or ZT-A30800D-10PLHR)

## What is LHR unlock dual mining mode?
You can now mine ETH (~30% of full speed) and other coins (~70%) simultaneously with LHR cards using their full potential.
Available combinations along with memory requirements:
* ETH+ERGO (8GB+)
* ETH+RVN (10GB+)
* ETH+CFX (10GB+)
See https://github.com/trexminer/T-Rex/wiki/LHR on how to set it up.
WebUI is not updated yet to reflect second algo stats in dual mode, but will be in future.

## Why does my GPU keep hitting LHR locks?
If you struggle to find overclock settings that don't trigger LHR and LHR tune value keeps going down - this is especially
relevant to dual mining mode - try reducing locked core clock (`--lock-cclock`) until it doesn't happen anymore. Pick
a safe LHR tune value (`--lhr-tune 20` for dual mining mode, `--lhr-tune 60` for ETH, `--lhr-tune 80` for ERGO), and lower
`--lock-cclock` until LHR no longer engages. Then try higher LHR tune values.

## What are the red numbers behind the "R:"?
That's the percentage of rejected shares. 
  
This is often an issue with your overclock settings being too aggressive, causing the card to be unstable.

## What does the red (!) mean?
After generating a DAG the miner computes its checksum. (!) next to it indicates that the checksum is invalid for the current epoch, and the DAG buffer is corrupted. 
  
The most common cause for this is excessive memory overclock. If the DAG buffer is corrupted, the affected GPU may produce invalid shares which will reduce your effective hashrate. 
  
Sometimes invalid shares percentage is very low and can be ignored, otherwise lower your memory overclock until (!) no longer appears.

## What do the temperature numbers in T-Rex mean?
This depends on the GPU, and what it exposes to the Nvidia driver.

T-Rex reports what it can see, in this order of preference:
* GPU and memory temp
* GPU and hotspot temp
* GPU temp only

Do not get confused between hotspot and memory temps. Hotspot temp is the highest temperature seen on the GPU die, and has nothing to do with memory temps.

GDDR6 has no memory temp sensors, and therefore there is no way for any tool to read the temps, while GDDR6X does have memory temp sensors, so those cards will show GPU and memory temps in T-Rex.

*Some cards with core/hotspot temperature sensors you can see in GPU-z will not expose the hotspot sensor via the native NVAPI calls; these cards will only report core temps via T-Rex due to the Nvidia driver limitations.*

Note: On Linux Nvidia only exposes the core temps via the Nvidia driver. There is currently no solution for this until Nvidia exposes this for their Linux drivers.

## Why can't I see memory temperatures in T-Rex?
You can only see things that the card exposes to the Nvidia driver, which is the fault of Nvidia, not T-Rex.

T-Rex simply uses the native NVAPI functions - these are only available on Windows.

## How do I create an API Key?
`--api-generate-key` does not automatically append/edit the JSON at the current moment, in the meanwhile we have to do it manually.
1. Open a CMD or terminal window and navigate to the T-Rex directory.
1. enter: ```t-rex --api-generate-key YourDesiredWebGuiPassword```
1. Another CMD window will open with your API key in it. Copy this key and use it in your `*.bat`/`*.sh` or config file as the value for the `--api-key` setting.
1. Run T-Rex as usual, navigate to http://127.0.0.1:4067, enter the password you used to create the key, and enjoy!

### OR
Create a bat file in your T-Rex directory, paste this code into it, run it, and use the generated key in your .bat/config file.
```
<@echo off
set /p password=Choose a password for your T-Rex api-key:
cls
echo Your api-key will be shown in a new window.
echo Highlight and right click it to copy the key.
echo Once it has been copied you may close that window.
echo.
echo.
pause
start T-Rex.exe --api-generate-key %password%
exit
```

## How do I use an API Key once I've created it?
### `*.bat`/`*.sh` file:
Add ```--api-key YourLongApiKeyGoesHere``` to your arguments, save, and run. 
### config file:
Put your API key in the empty quotes behind the ```"api-key" : "YourLongApiKeyGoesHere",``` setting, save, and run.
                                  
When you load the web gui, it will ask you for your password. Enter the same password you entered when you generated your api key.

## Why can't I save settings in the WebUI?
You probably don't have a config file in the T-Rex directory, or you forgot to launch T-Rex with the -c (--config) option.

Copy-paste or rename the ```config_example``` sample file to something like ```config.json``` and add ```--config config.json``` to your batch file.

## Where can I see WebUI for my miner?
Open http://127.0.0.1:4067/ (or [localhost](http://localhost:4067)) in a web browser on the mining machine.

## How do I see the T-Rex WebUI from another computer or phone on my local network?
If you cannot see your T-Rex WebUI from another computer on your local network, it is most likely due to a firewall issue on the computer doing the mining. 
  
To open the default port (TCP port 4067) T-Rex uses for incoming connections, follow the instructions below.

**Windows:**
1. On the miner, go to Start > Run and type firewall.cpl to open the Windows Firewall window.
1. Click on the "Advanced Settings" link on the left pane. The Windows Firewall with Advanced security window opens.
1. Click on the "Inbound Rules" option.
1. On the right pane, click on "New rule".
1. Under "Rule Type" select the option "Port" and click next.
1. Select "TCP" and "specific local ports" options.
1. Enter 4067 in the specific local ports box and click next.
1. Select the option "Allow the connection" and click next.
1. Click next. (leave the three boxes checked)
1. Enter T-Rex in the Name field and click Finish.

**Linux (using UFW):**
1. From a terminal window do: ```sudo ufw allow from any to any port 4067 proto tcp``` 
1. To verify the rule was added correctly, do: ```sudo ufw status```

## What do the lines on the graph mean?
The newer versions of T-Rex have both a mouseover tooltip and a key at the bottom to show what the colors mean.
  
In older versions that don't have these features, grey is power, blue is hashrate, red is average power, and green is average hashrate.

## Where do I find the best OC (overclock) settings for my GPU?
Visit [WhatToMine](https://www.whattomine.com/) and move your mouse over your graphics card. A tooltip will appear showing some sample overclock settings that should get you started.

Note, when there are two memory values listed, the lower one is for Windows, and the doubled-value is for Linux. Do **not** use a Linux memory setting in Windows.

The best thing to do is to learn how to overclock for yourself, per card and algorithm combination that you're mining, and one of our Discord community members has a couple **great** videos on how to do just this!
* https://www.youtube.com/watch?v=7JGcQLgV5Gw
* https://www.youtube.com/watch?v=0F4xxcCAJVI

Watch these, and follow along *so you have an understanding* of how to overclock safely.

If you have a 30XX series card (or a different GPU that has ECC memory) and you'd like to monitor your card for errors while you perform your overclock, open a CMD window and send the command ```nvidia-smi dmon -s pucvmet``` and watch the appropriate columns for ECC errors.

## Why does my hashrate go lower when I keep increasing my `--mclock` value?
It's ECC memory. If it is producing errors, it has to fix them, which costs performance.

It's doing exactly what it should do. You can see the errors by opening a CMD window and send the command ```nvidia-smi dmon -s pucvmet``` to verify.

## What is the difference between `--lock-cclock` and `--cclock`?

* `--lock-cclock` sets the core clock to an absolute value
* `--cclock` is an offset (+/-) from what the clock runs at normally 
* `--lock-cclock` manages power to keep the core clock where you set it
* `--cclock` does not manage power, so you would need to use the `--pl` setting to do that
* `--lock-cclock` and `--cclock` are mutually exclusive, so disable one or the other if you are using both on a multi-card rig (ie: `--lock-cclock 0,1200 --cclock 100,0`)

## What intensity or kernel should I use?
T-Rex will run a benchmark when it's started and pick the best settings to run at. If you are using an external application to overclock your card(s), make sure you apply your overclock settings before you start T-Rex. If you're using T-Rex to overclock, it will do so before benchmarking.
  
If you experience hashrate drop between releases make sure that the miner selects same kernel. If kernel differs for the new version then set proper kernel manually by adding a --kernel parameter to the T-Rex startup arguments.

## How do I run a benchmark?
For ETHash, you can start T-Rex with ```t-rex -a ethash --benchmark --benchmark-epoch 446``` and it will give you more reports on how fast it's working. This is great for tuning your cards. 
  
Benchmark values for some other algos:
* kawpow: ```--benchmark --benchmark-block 1970248```
* autolykos2: ```--benchmark --benchmark-block 596150```
* conflux: ```--benchmark --benchmark-epoch 50```
  
To make it easier to find the average with fluctuating hashrates, you can add ```--hashrate-avr 300``` which will smooth out the hashrates after about five minutes based on the total average.  

## How does memtweak work?
Memory tweak mode works similar to ETHlargementPill. It is supported on Pascal GPUs with GDDR5 or GDDR5X memory only. 
       
See the readme file for instructions on how to use the `--mt` parameter.

## High CPU usage
If you experience high CPU usage by T-Rex miner process on Windows and your NVIDIA drivers are 471.11 or newer, the most likely cause is the "Hardware-accelerated GPU Scheduling" feature. 
  
To disable it, go to Start -> Settings -> Display -> Graphics settings, and turn it off.

## What are error codes 15 and 999?
These errors usually indicate hardware related problems (risers, power supply, cabling etc.), see more details at: https://www.cryptoprofi.info/?p=5519

## I'm getting a "code -6":
`-6` translates into the following NVAPI error code: ```NVAPI_NVIDIA_DEVICE_NOT_FOUND | No NVIDIA display driver, or NVIDIA GPU driving a display, was found.```

**Code -6 memory tweak errors usually point to a driver problem.**
                                                                                                                                                  
* Use something like DDU (DisplayDriverUninstaller) to fully remove all Nvidia drivers
* Restart the system 
* Install the new driver directly from the Nvidia website
* Restart the system again
                                                                                                                                                  
**Code -6 BusID errors almost always point to a power/riser issue.**

## What is the "instance wasn't validated" error? 
Right after the miner starts there must be an internet connection to the developers server for miner validation. If you set firewall rules to restrict outgoing connections this can be the reason of the problem. 

## T-Rex reports very high VRAM temps, is this safe?
That all depends on the silicon your GPU has.

For cards with GDDR6X VRAM (ie: 3070 Ti, 3080, 3080 Ti, 3090), it is generally recommended to stay below 95C on memory junction temps which is shown as the second temp value in T-Rex. This is a good resource for these cards:
https://www.youtube.com/watch?v=ph4_Sr8YNXI

## I'm getting a "No connection" error, but my network connection is fine
This usually happens when Windows Firewall blocks network connections initiated by T-Rex. To allow T-Rex though the firewall follow these steps:
1. Press Start
2. Type ```firewall.cpl``` and press Enter
3. Select "Allow an app or feature through Windows Defender Firewall" on the left side of the window
4. Click "Change settings"
5. Click the "Allow another app..." button
6. Click the "Browse..." button
7. Browse to the location of your t-rex.exe
8. Highlight `t-rex.exe` and press the "Open" button
9. Click "Add"
10. Click "OK"
11. Reboot

Another possible reason, if you're based in mainland China, is DNS tampering. In order to circumvent that, run
the miner with `--no-sni --dns-https-server 1.1.1.1` parameters.

## Why does `--autoupdate` not work?
It only works for T-Rex 0.23.0+. There was a breaking change in 0.23.0 so auto updates was disabled for any version older than that.
       
**IMPORTANT!** If you are running a version older than 0.23.0, be sure to remove your overclock settings before updating! The cards may likely be numered/logged into a different order so your overclocks will end up on different cards than you intend. You can reapply them in the correct order after update has been completed.

## Why are some of my config.json settings not working?
If you specify any commands in your batch file aside from `--config config.json` you will not be able to change those you do specify beyond that.
       
ie: ```--config config.json --api-key XXXX``` will allow you to change every value and save them to config.json except for a new API key when you try to change the password via the WebUI. 

### Other options:
**Windows command (CMD):**

Open a command window and use this command (use your own IP and password)
```
for /f usebackq^ tokens^=4^ delims^=^" %a in (`"curl -s http://IP_OF_RIG_HERE:4067/login?password=PASSWORD_GOES_HERE"`) do @echo %a && curl "http://IP_OF_RIG_HERE:4067/control?sid=%a&pause=true"
```
  
**Windows .bat to pause T-Rex:**

Create a .bat file containing the following lines and run it.
```
:: bat to pause T-Rex
@echo off
set /p password=Enter your T-Rex password:
for /f usebackq^ tokens^=4^ delims^=^" %%b in (`"curl -s http://localhost:4067/login?password=%%password%%"`) do (curl -s "http://localhost:4067/control?sid=%%b&pause=true")
pause
```
  
**Windows ".bat" to unpause T-Rex:**

Create a `*.bat` file containing the following lines and run it.
```
:: bat to unpause T-Rex
@echo off
set /p password=Enter your T-Rex password:
for /f usebackq^ tokens^=4^ delims^=^" %%b in (`"curl -s http://localhost:4067/login?password=%%password%%"`) do (curl -s "http://localhost:4067/control?sid=%%b&pause=false")
pause
```
  
**LINUX coreutils + cURL:**
```
curl -s "http://IP_OF_RIG_HERE:4067/control?sid=`curl -s 'http://IP_OF_RIG_HERE:4067/login?password=PASSWORD_GOES_HERE'|cut -f4 -d'"'`&pause=true"
```

For a specific card in a rig ```&devices=ID_OF_CARD```

For mutliple cards in a rig ```&devices=ID_OF_CARD,ID_OF_OTHER_CARD,ETC```

Append the above after ```pause=true``` / ```pause=false``` when pausing specific devices
