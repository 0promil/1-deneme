As of T-Rex version 0.24.0 you have two options of how to use your LHR cards:

## Option 1: "dual mining" LHR unlock

This option allows you to use the full potential of LHR cards that have enough VRAM to hold two DAGs/datasets by mining
two cryptocurrencies simultaneously - ETH (~30%) and some other (~70%).


**Quick start**: see "LHR-unlock" dual mining ready `*.bat`/`*.sh` files in the miner archive on how to run it. If you are using HiveOS 
or any other mining OS that launches T-Rex with a config file rather than command line arguments, you need to specify
your parameters in JSON, for example:
```
"lhr-algo": "octopus"
"url2": "stratum+tcp://pool.woolypooly.com:3094"
"user2": "cfx:aajauymfc0cpd4aj91wmfyd150avfg3fmym9j2xrh8.rig0"
"pass2": "x"
```
The above will set `octopus` as the second algo in dual mining mode.

**Video guide**: https://youtu.be/7JwtKNiKdIM

Various coins have different memory requirements, so below you will find a list of available combinations along with
memory requirements at the time of writing.    
Some figures on what you can expect to achieve (all done with `--lhr-tune 30` which is the default):

### ETH+ERGO

Requires 8GB+ VRAM.  
ERGO is known to be affected by LHR and for most GPUs it's a matter of finding overclock settings that don't trigger LHR
when mining ERGO on its own (single mode), and then use the same settings for ETH+ERGO dual mode.  

**Important**: if your GPU is LHR-constrained on ERGO in single mode no matter what overclock you set, this dual
mode is not for you as the miner will be constantly hitting LHR locks.

| GPU         | ETH hashrate | ERGO hashrate | Power limit           | Overclock settings                                  |
| ----------- | ------------ | ------------- | --------------------- | --------------------------------------------------- |
| 3080Ti      | 35.4 MH/s    | 183.3 MH/s    | PL 82% (287W)         | mem +1000 (linux +2000), core 0                     |
| 3080        | 31.8 MH/s    | 153.0 MH/s    | ~240W (locked clock)  | --lock-cclock 1580, mem +1525 (linux +3050), core 0 |
| 3070Ti      | 23.1 MH/s    | 123.9 MH/s    | ~170W (locked clock)  | --lock-cclock 1540, mem +1300 (linux +2600), core 0 |
| 3060        | 12.5 MH/s    | 74.5 MH/s     | ~90W  (locked clock)  | --lock-cclock 1250, mem +1300 (linux +2600), core 0 |

### ETH+RVN, ETH+FIRO

Requires 10GB+ VRAM.  
| GPU         | ETH hashrate | RVN hashrate  | Power limit           | Overclock settings                                  |
| ----------- | ------------ | ------------- | --------------------- | --------------------------------------------------- |
| 3080Ti      | 35.7 MH/s    | 29.6 MH/s     | PL 82% (287W)         | mem +1000 (linux +2000), core 0                     |
| 3060        | 14.8 MH/s    | 13.9 MH/s     | PL 60% (102W)         | mem +1300 (linux +2600), core 0                     |

### ETH+CFX

Requires 10GB+ VRAM.  
| GPU         | ETH hashrate | CFX hashrate  | Power limit           | Overclock settings                                  |
| ----------- | ------------ | ------------- | --------------------- | --------------------------------------------------- |
| 3080Ti      | 36.4 MH/s    | 60.6 MH/s     | PL 82% (287W)         | mem +1000 (linux +2000), core 0                     |
| 3060        | 14.9 MH/s    | 26.7 MH/s     | PL 60% (102W)         | mem +1300 (linux +2600), core 0                     |


This section will be updated as more people provide their feedback on what settings are found to be stable.

## Option 2: "standard" LHR unlock

### ETH
T-Rex has partial LHR unlock functionality for 30xx GPUs mining `ethash` (~78% of full hashrate).  

* LHR mode is enabled by default for LHR cards, however, if you want to override LHR card auto-detection, you can do
so by specifying `--lhr-tune` parameter which takes values from -1 to 100:  
`-1` - auto  
` 0` - disabled (use for non-LHR cards)  
`74` - recommended starting value for most LHR cards in low power mode (see `--lhr-low-power`)  
`78` - recommended starting value for most LHR cards  
It can also be set for each GPU separately, e.g. `--lhr-tune 0,0,77.5,0` - this will tell the miner that the third GPU
is LHR and that it needs to start with the tuning value of `77.5`, while the rest of the cards are non-LHR.  
HiveOS equivalent would be `"lhr-tune": "0,0,77.5,0"`

### ERGO
ERGO mining, as opposed to ETH, isn't targeted by LHR so its effect is not as pronounced.  

* In order to enable LHR unlocker you need to explicitly tell the miner which GPUs are LHR limited at your current settings.  
Commonly used LHR tune values:  
` 0` - disabled (use for non-LHR cards, or the ones that aren't affected by LHR under the overclock you use)  
`80` - GPUs with GDDR6 Hynix memory, these aren't working well with the unlocker, so you may need to try even lower setting  
`91` - good starting point for GPUs with GDDR6 non-Hynix memory  
`99` - use this value for your GDDR6X GPUs if you found it tricky to tweak OC settings not hitting LHR

## Tips

* Previously, when T-Rex tried to unlock LHR cards, by default it used "LHR auto-tune" feature where it increased
LHR tune automatically if the GPU was stable and didn't hit LHR at the current tune value. It also decreased
the tune value if it hit LHR too frequently. Starting from version 0.25.15 LHR auto-tuner is working in "down" mode
by default meaning it won't go up on its own, only down. To bring the old behaviour back use `--lhr-autotune-mode full`.
If you want to disable auto-tune completely and keep LHR tune value constant, run the miner with `--lhr-autotune-mode off`.

* It's important **not** to set intensity values manually as that may interfere with the unlocking algorithm.

* The miner will try to achieve reasonable hashrate levels using the provided settings, and if that's not possible, 
will start aiming lower. During this process the reported hashrate will fluctuate and mostly stay on the lower side
because every LHR lock will cause the miner to pause for 20 seconds to unlock the GPU, so you may need to wait till
it finds stable settings.

* Hashrate will be fluctuating even more wildly in dual mining mode. You can increase hashrate averaging window and
smooth out the fluctuations by using `-N` parameter, for example `-N 180` will tell the miner to report 3 minute average
hashrate as opposed to 1 minute average (which is the default).

* Don't change your overclock settings too much while the miner is running, particularly be careful with the changes
that may result in a rapid hashrate drop, like reducing memory overclock or decreasing power limit significantly
(all during mining) - this can trick the miner into thinking the LHR has kicked in.

* If you struggle to find overclock settings that don't trigger LHR and LHR tune value keeps going down, try reducing
locked core clock (`--lock-cclock`) until it doesn't happen anymore.