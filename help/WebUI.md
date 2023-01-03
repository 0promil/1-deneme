# Accessibility

T-Rex comes with a built-in web monitoring/control page.
By default, it is only accessible from the same PC where the miner is running - http://127.0.0.1:4067/.
If you would like to use it from other machines in your local network you need to set `--api-bind-http` parameter, e.g.
`--api-bind-http 192.168.0.15:4067` - replace IP address with yours. Alternatively, to bind to ALL available network interfaces, use `--api-bind-http 0.0.0.0:4067` - the URL to access the monitoring page will appear in the miner console.

# Security

By default, T-Rex WebUI provides read-only access to your mining statistics information and rig configuration.
In order to be able to modify/update the settings, you need to set up a password as a security measure to prevent others
changing your miner configuration.  

Steps to set up WebUI password:
1. Open command prompt and navigate to the directory where the miner executable is.
2. Run `t-rex --api-generate-key <your_password>`.  
The password must be 8-64 characters long, without spaces, and must
contain at least one digit, lowercase, and uppercase letters.  
(Windows) If a new command prompt opens and quickly closes, go to step 1 and run the command prompt under Administrator.
3. The output from step 2 is your API key, and it needs to be added as an extra T-Rex parameter in your `*.bat`/`*.sh`
script:  
`--api-key <generated_key>`
4. Start the miner. Now when you try to access WebUI, it will prompt you to enter the password that you used in step 2.

Steps 2 and 3 can be combined into one if you use T-Rex with a config file: run
`t-rex --api-generate-key <your_password> -c <your_config_file>` and the generated key will be inserted into your
config file automatically.

**Note:** there is no way to recover your password from the API key, so if you forget it, regenerate the key using a
new password.

# Creating a config file

If you don't have a config file, you can extract it from a running T-Rex instance:  
On the rig navigate to http://localhost:4067/, click the cog icon > raw config > get > copy the config from that page to a new file named `config.txt`.  
You can backup your original batch file and then modify the original file.  
Replace the line with `t-rex.exe` on it with this: `start t-rex.exe --config config.txt`  
_Optional: Remove pause as well to have only one console open._

# Config modification

At the moment, changing miner configuration is only possible if you've started the miner using config file
(`t-rex --config <config_file>`) as opposed to setting command line arguments in `*.bat`/`*.sh` scripts - see config file
example in the miner archive, it's called `config_example`.  
Applying the changes for most parameters exposed on Settings page requires miner restart. You will be prompted to do so
after clicking "SAVE SETTINGS" button. "RESTART MINER" button is the top of the page and will be glowing red.

# Customisation

If you prefer the look of our old WebUI, download [webui.zip](https://github.com/trexminer/T-Rex/releases/download/0.23.1/webui.zip),
put it next to T-Rex executable, and restart the miner. It will automatically start using the old monitoring page.
Alternatively, you can develop your own UI - use the old UI archive as a template. All HTML, JS, and CSS files must
be in a ZIP archive called `webui.zip` for the miner to pick it up.