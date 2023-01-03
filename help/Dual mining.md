GPU miners can benefit from the fact that some algorithms are memory-heavy (like `ethash`) and others are core-heavy
(like `blake3`) making it possible to combine them and mine the secondary algorithm at very little impact
to the primary algorithm hashrate.  

Dual mining can be enabled with `--dual-algo` parameter which should be preferred over the deprecated `--lhr-algo`.

## ETHW+ALPH, ETC+ALPH

**Quick start**: see "ETHW+ALPH" `*.bat`/`*.sh` file in the miner archive on how to run it. If you are using HiveOS
or any other mining OS that launches T-Rex with a config file rather than command line arguments, you need to specify
your parameters in JSON, for example:
```
"dual-algo": "blake3"
"url2": "stratum+tcp://pool.woolypooly.com:3106"
"user2": "1qUuxVuXN2Pk4nnYTbL4qihjLWyRkVMQVYQDAajCcuPq"
"pass2": "x"
```
The above will set `blake3` as the second algo in dual mining mode.


### Behaviour and tuning
There are a few options to control the behaviour and fine-tune the performance of the GPUs in respect to how they 
dual mine. See the options below:  

> `--dual-algo-mode <algo>:<tuning coefficient>`

`<algo>` can be one of the following:  
* `a1` - the GPU will be mining just the primary algorithm (ethash)  
* `a2` - the GPU will be mining just the secondary algorithm (the one you set in `--dual-algo`)  
* `a12` - the GPU will be mining both algorithms at the same time (dual mining)  

`<tuning coefficient>` is optional, and can be one of the following:

| Tuning coefficient | GPU type | Description                                  | Formula                                                     |
|--------------------|----------|----------------------------------------------|-------------------------------------------------------------|
| `rXX`              | non-LHR  | "dual ratio" `XX`                            | `H2 = H1 * <dual ratio>`                                    |
| `hXX`              | non-LHR  | primary algo hashrate percentage `XX`%       | `H1 = H1_max * <hashrate percentage> / 100.0`               |
| `rXX:lrYY`         | LHR      | "dual ratio" `XX` <br> "LHR dual ratio" `YY` | `H2 = H1 * <dual ratio> + (H1_max - H1) * <LHR dual ratio>` |

where  
`H1` - primary algorithm hashrate  
`H2` - secondary algorithm hashrate  
`H1_max` - maximum theoretical primary algorithm hashrate  

Default value for `--dual-algo-mode` is `a12`, meaning all GPUs will be mining in dual mode with default settings - 
non-LHR will try to maintain 98% of the primary algorithm maximum hashrate, and LHR ones will be dual mining at
LHR 74 unless LHR tune values are explicitly set to a different value.


> `--profit-per-mh <profit_algo1>:<profit_algo2>`

`<profit_algo1>` is the amount of dollars (or any other currency) that you expect to earn by mining the primary 
algorithm at a speed of 1MH/s - you can get this info from an online mining calculator, `<profit_algo2>` - 
same for the secondary algorithm.  
Assuming you haven't set the dual ratio explicitly, this parameter will cause the miner to benchmark various "dual ratios" 
upon start up and choose the one that produces the highest earnings. This feature is only applicable to non-LHR cards. 
Your LHR cards will be dual mining according to the specified LHR tune values.  

#### Example
Consider the following set of parameters, assuming they are part of a ETHW+ALPH config:  
```
--dual-algo-mode a2,a1,a12,a12:r15:lr19,a12:r15,a1,a12:h95,a12
--lhr-tune 0,74,73,72,0,0,0,0
--profit-per-mh 0.0516:0.0012
```
This config translates into the following:

GPU#0: non-LHR, mines ALPH  
GPU#1: LHR, mines ETHW with LHR 74  
GPU#2: LHR, mines ETHW+ALPH with LHR 73  
GPU#3: LHR, mines ETHW+ALPH with LHR 72, dual ratio 15, LHR dual ratio 19  
GPU#4: non-LHR, mines ETHW+ALPH with dual ratio 15  
GPU#5: non-LHR, mines ETHW  
GPU#6: non-LHR, mines ETHW+ALPH with ETHW hashrate being approximately 95% of its max value in single mode  
GPU#7: non-LHR, mines ETHW+ALPH with dual ratio that maximises profitability based on the data set in `--profit-per-mh`
(ETHW expected profit is $0.0516/MH, ALPH - $0.0012/MH)

## Tips

* Due to its nature dual mining is very power hungry, so if you want to maximise your secondary algo hashrate try
raising the power limit. An even better way would be to leave the power limit at max and lock the core clock instead,
for the GPUs that support it.
* Do not forget to restart the miner after changing overclock settings.