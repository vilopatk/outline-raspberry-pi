How to use Outline key from command line on Raspberry Pi or any other Linux


1. **Install [Shadowsocks](https://github.com/shadowsocks/shadowsocks-rust):**


`sudo snap install shadowsocks-rust`\
Or get it from Github\
Create the configuration file:\
`touch config.json`\
Contents of the config.json file:

```json
{
"server": "<SERVER_ADDRESS>",
"server_port": <PORT>,
"local_port": 1080,
"password": "<PASSWORD>",
"timeout": 60,
"method": "<METHOD>"
}
```
Obtain data from your outline key:

`ss://Y2hhY2hhMjAtaWV0Zi1wb2x5MTMwNTpwYXNzd29yZA@example.com:5855`\
Decode password and method. Python example:
```python
import base64

base64.b64decode(b'Y2hhY2hhMjAtaWV0Zi1wb2x5MTMwNTpwYXNzd29yZA')
# Output: b'chacha20-ietf-poly1305:password'
```
Where:

* SERVER_ADDRESS: example.com
* PORT: 5855
* PASSWORD: password
* METHOD: chacha20-ietf-poly1305
2. **Install ProxyChains:**

`sudo apt-get install proxychains`\
Edit the ProxyChains configuration:

`sudo nano /etc/proxychains.conf`\
Add the following to the configuration:\
`socks5 127.0.0.1 1080`\
Remove preconfigured proxies if they exist.

3. **Run Shadowsocks:**

`sslocal -c path/to/config/file/config.json`

4. **Run your application using ProxyChains:**

`proxychains ping google.com`