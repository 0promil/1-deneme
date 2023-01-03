By default HTTP API server binds to `127.0.0.1:4067`. It means that you can only access your miner from localhost.
See `--api-bind-http` parameter on how to change it.
Common example of request structure: `http://<ip>:<port>/<handler_name>`

Handlers:
* **trex** - Shows miner control monitoring page in your web browser.  
  You can see miner stats in real time and also change miner parameters and config on the fly. Aside from that you will also see any available updates.

* **login** - Intended to get session id key to use with all requests in case the miner was protected with api-key.
  `http://127.0.0.1:4067/login?password=your_password`  =>  `{"sid":"hj2DGIIYQ6rWcEbtscEU0ooGQvj3101L","success":1}`
  Then use "sid" with every request.
  `http://127.0.0.1:4067/summary?sid=hj2DGIIYQ6rWcEbtscEU0ooGQvj3101L`
  
* **logout** - Intended to logout active session.
  `http://127.0.0.1:4067/logout?sid=hj2DGIIYQ6rWcEbtscEU0ooGQvj3101L`  

* **config** - Changes your config on HDD and also change some miner parameters on the fly.  
  You can change multiple parameters with one request. Both GET and POST requests supported.  
  If you use a config file (e.g. `t-rex.exe -c config_file`), then any action with handler `config` will be saved into `config_file`.  
  You can use this handler for automation like changing config file at run-time, shutting down the miner via API and then restarting it with new parameters applied.

  GET usage examples:
    * `http://127.0.0.1:4067/config?protocol-dump=true`   
      Enables protocol dump on the fly and write it into config_file
    * `http://127.0.0.1:4067/config?algo=x16r&devices=0,1&intensity=20,21`   
      Writes the following config settings into the config file: `algo=x16r`, `devices=0,1`, `intensity=20,21`
    * `http://127.0.0.1:4067/config?algo=x16r&devices=0,1&intensity=20,21&config=test.conf`   
      Saves settings into the file `test.conf` which will be created in the folder where the miner resides: `algo=x16r`, `devices=0,1`, `intensity=20,21`
    * `http://127.0.0.1:4067/config?config=test.conf`   
      Saves your current miner settings into `test.conf` file
    * `http://127.0.0.1:4067/config`   
      Shows the current config state
    * `http://127.0.0.1:4067/config?hashrate_avr=10&temperature-limit=70&temperature-start=40`   
      Sets the following parameters on the fly: `hashrate_avr=10`, `temperature-limit=70`, `temperature-start=40`

  For POST requests you must use correct json object with parameters you want to change:  
  URL: `http://127.0.0.1:4067/config`.   
  Payload: `{"hashrate_avr": 10, "temperature-limit": 70, "temperature-start": 40}`.  
  Parameter names and types in json are identical to config json you normally use.


* **summary** - Shows all information about current mining process.

Response example with comments:
``` json5
{
  // Number of accepted shares count
  "accepted_count": 6,
  
  // Information about the pool your miner is currently connected to
  "active_pool":
  {
    // Current pool difficulty
    "difficulty": 5,
    
    // Pool latency
    "ping": 97,
    
    // Number of connection attempts in case of connection loss
    "retries": 0,
    
    // Pool connection string
    "url": "stratum+tcp://...",
    
    // Usually your wallet address
    "user": "..."
  },
  
  // Algorithm which was set in config
  "algorithm": "x16r",

  // HTTP API protocol version   
  "api": "1.2",

  // CUDA toolkit version used to built the miner
  "cuda": "9.10",

  // Software description
  "description": "T-Rex NVIDIA GPU miner",
  
  // Current network difficulty
  "difficulty": 31968.245093004043,

  // Total number of GPUs installed in your system
  "gpu_total": 1,
  
  // List of all currently working GPUs in your system with its stats
  "gpus": [{
    // Internal device id, useful for devs
    "device_id": 0,                        

    // Fan blades rotation speed in % of the max speed
    "fan_speed": 66,                       

    // User defined device id in config
    "gpu_user_id": 0,                        

    // Average hashrate per N sec defined in config
    "hashrate": 4529054,                   

    // Average hashrate per day
    "hashrate_day": 5023728,    

    // Average hashrate per hour
    "hashrate_hour": 0,          

    // Average hashrate per minute
    "hashrate_minute": 4671930,    

    // User defined intensity
    "intensity": 21.5,        

    // Current device name.
    "name": "GeForce GTX 1050",

    // Current device temperature.
    "temperature": 80,            

    // Current device vendor.
    "vendor": "Gigabyte", 

    // Device state. Might appear if device reached heat limit. (set by --temperature-limit)
    "disabled":true,                       

    // Device temperature at disable. Might appear if device reached heat limit.
    "disabled_at_temperature": 77,
    
    // Shares stat for the device.
    "shares": {
        "accepted_count": 3,
        "invalid_count": 0,
        "rejected_count": 0,
        "solved_count": 0
    }
  }],
  
  // Total average sum of hashrates for all active devices per N sec defined in config.
  "hashrate": 4529054,                       

  // Total average sum of hashrates for a day.
  "hashrate_day": 5023728,                   

  // Total average sum of hashrates for an hour.
  "hashrate_hour": 0,                        

  // Total average sum of hashrates for a minute.
  "hashrate_minute": 4671930,                

  // Application name
  "name": "t-rex",

  // Operating system
  "os": "linux",

  // This is number of rejected shares count.
  "rejected_count": 0,                       

  // This is number of found blocks.
  "solved_count": 0,                

  // Current time in sec from the beginning of the epoch. (ref: https://www.epochconverter.com)
  "ts": 1537095257,                          

  // Uptime in sec. This shows how long the miner has been running for.
  "uptime": 108,                             

  // Miner version.
  "version": "0.6.5",

  // Information about available update. Appears in case update is available.
  "updates":{                                

    // Url of file archive to download.
    "url": "https://fileurl",          

    // Signature of update pack (md5).
    "md5sum": "md5...",               

    // T-Rex version in update.
    "version": "0.8.0",        

    // Short info about changes in update.
    "notes": "short update info",         

    // Whole info about changes in update.
    "notes_full": "full update info",     

    // Information about current update download.
    "download_status":
    {
      // Total bytes downloaded.
      "downloaded_bytes": 1775165,

      // Total bytes to download.
      "total_bytes": 5245345,

      // Last error if download failed.
      "last_error":"",

      // Time elapsed since first byte downloaded.
      "time_elapsed_sec": 2.887111,

      // Download service state.
      "update_in_progress": true,

      // Download service named state. ("started", "downloading", "finished", "error", "idle")
      "update_state": "downloading",

      // Url of file in operation.
      "url": "https://fileurl"
    },
  }
}
```

* **do-update** - Updates the miner.  
  Navigate to `http://127.0.0.1:4067/do-update` to start T-Rex update.  
  Navigate to `http://127.0.0.1:4067/do-update?stop=true` to stop the update.


* **control** - Real time configuration of T-Rex miner.  
  As of API 1.3 version the following commands are supported:

  * _shutdown_ - Shuts down your miner. Usage: `http://127.0.0.1:4067/control?command=shutdown`.   
  If you prefer POST set the request body to `{"command": "shutdown"}`.
  
  * _pause_ - Stops your miner. Usage: `http://127.0.0.1:4067/control?pause=true` ; to resume use: `http://127.0.0.1:4067/control?pause=false`.   
  To pause certain GPUs: `http://127.0.0.1:4067/control?pause=true:0,2,3` ; to resume use: `http://127.0.0.1:4067/control?pause=false:0,2,3`.   
  If you prefer POST set the request body to `{"pause": "true:0,2,3"}`.

  * _hashrate-avr_ - Changes sliding window size in real time. Usage: `http://127.0.0.1:4067/control?hashrate-avr=1`.   
  It will set sliding window of size 1 sec.   
  If you prefer POST set the request body to `{"hashrate-avr": 1}`.

  * _no-color_ - Disables color output to console. Usage: `http://127.0.0.1:4067/control?no-color=true`. To enable: `http://127.0.0.1:4067/control?no-color=false`.   
  If you prefer POST set the request body to `{"no-color": true}`.

  * _protocol-dump_ - Enables user protocol dump into console/log. To enable: `http://127.0.0.1:4067/control?protocol-dump=true`. To disable: `http://127.0.0.1:4067/control?protocol-dump=false`.   
  If you prefer POST set the request body to `{"protocol-dump": true}`.

  * _time-limit_ - Sets time limit in seconds for miner (it will shutdown after timeout). Usage: `http://127.0.0.1:4067/control?time-limit=120`. It will shutdown your miner 120 seconds after this request.   
  To disable: `http://127.0.0.1:4067/control?time-limit=0`.   
  If you prefer POST set the request body to `{"time-limit": 120}`.
