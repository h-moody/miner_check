# Antminer L7 and E9 pro Monitoring Script

This project is a Python script designed to monitor the status of Antminer devices (E9 Pro and L7 models). The script checks miner availability, temperature, wallet address, and hash rate, sending alerts through Telegram if issues are detected.

## Features
- **Ping Test**: Checks if miners are reachable.
- **Wallet Address Verification**: Confirms that miners are mining to the correct wallet address.
- **Temperature Monitoring**: Monitors CHIP and PCB temperatures, and sends alerts if they exceed safe levels.
- **Hashrate Monitoring**: Tracks the 5-second and 30-minute average hash rate, notifying if the rates are below defined thresholds.
- **Telegram Notifications**: Alerts are sent via Telegram to inform about critical issues.
- **Logging**: Logs all activities to a log file and also displays them in the console.

## Prerequisites
- Python 3.x
- Required Python libraries: `requests`

You can install the required libraries with:
```sh
pip install requests
```

## Installation
1. **Clone the Repository**
   ```sh
   git clone https://github.com/h-moody/miner_check.git
   cd miner_check
   ```

2. **Set Up Virtual Environment**
   It is recommended to create a virtual environment to manage dependencies.
   ```sh
   python -m venv venv
   source venv/bin/activate  # On Windows use: venv\Scripts\activate
   ```

3. **Install Dependencies**
   Install the necessary dependencies listed in the `requirements.txt` file.
   ```sh
   pip install -r requirements.txt
   ```

## Configuration
You can store the miner credentials, IP addresses, temperature thresholds, hash rate thresholds, Telegram bot token, and other settings in a configuration file to easily manage and run the script.

### Example Configuration File
Create a JSON configuration file, e.g., `config.json`, with the following content:
```json
{
  "username": "root",
  "password": "root_password",
  "telegram_token": "YOUR_TELEGRAM_BOT_TOKEN",
  "chat_id": "YOUR_CHAT_ID",
  "e9_ips": [
    "172.16.253.201",
    "172.16.253.202"
  ],
  "l7_ips": [
    "172.16.253.101",
    "172.16.253.102"
  ],
  "wallet_e9": "YOUR_E9_WALLET_ADDRESS",
  "wallet_l7": "YOUR_L7_WALLET_ADDRESS",
  "wallet_prefix_l7": "YOUR_L7_WALLET_PREFIX",
  "max_temp_e9": 84,
  "max_temp_l7": 80,
  "min_hashrate_5s_e9": 100,
  "min_hashrate_30m_e9": 3300,
  "min_hashrate_5s_l7": 100,
  "min_hashrate_30m_l7": 8000
}
```

## Running the Script
To run the script, you can either provide the required parameters through command-line arguments or use a configuration file.

### Example Usage with Configuration File
```sh
python miner_check.py --config config.json
```

### Example Usage with Command-Line Arguments
```sh
python miner_check.py \
  --username root \
  --password root_password \
  --telegram_token YOUR_TELEGRAM_BOT_TOKEN \
  --chat_id YOUR_CHAT_ID \
  --e9_ips 172.16.253.201 172.16.253.202 \
  --l7_ips 172.16.253.101 172.16.253.102 \
  --wallet_e9 YOUR_E9_WALLET_ADDRESS \
  --wallet_l7 YOUR_L7_WALLET_ADDRESS
```

### Parameters
- `--config`: Path to a JSON configuration file (optional).
- `--username`: Username for miner authentication (optional if provided in config).
- `--password`: Password for miner authentication (optional if provided in config).
- `--telegram_token`: Telegram bot token for sending messages (optional if provided in config).
- `--chat_id`: Telegram chat ID where messages will be sent (optional if provided in config).
- `--e9_ips`: List of IP addresses of the E9 Pro miners to be monitored (optional if provided in config).
- `--l7_ips`: List of IP addresses of the L7 miners to be monitored (optional if provided in config).
- `--wallet_e9`: Wallet address for E9 Pro miners (optional if provided in config).
- `--wallet_l7`: Wallet address for L7 miners (optional if provided in config).
- `--wallet_prefix_l7`: Wallet address prefix for L7 miners (optional if provided in config).
- `--max_temp_e9`: Maximum CHIP temperature for E9 Pro miners (default: 84°C).
- `--max_temp_l7`: Maximum CHIP temperature for L7 miners (default: 80°C).
- `--min_hashrate_5s_e9`: Minimum 5-second hashrate for E9 Pro miners (default: 100 MH/s).
- `--min_hashrate_30m_e9`: Minimum 30-minute hashrate for E9 Pro miners (default: 3300 MH/s).
- `--min_hashrate_5s_l7`: Minimum 5-second hashrate for L7 miners (default: 100 MH/s).
- `--min_hashrate_30m_l7`: Minimum 30-minute hashrate for L7 miners (default: 8000 MH/s).

## Logging
- **File Logging**: All logs are saved to `miner_logs.log`.
- **Console Logging**: Logs are also displayed in the console for real-time monitoring.

## Customization
### Wallet Address Check
- The script verifies wallet addresses for miners.
- For L7 miners, wallet addresses can either be provided as a fixed address or generated based on the miner's IP address in the format `<wallet_prefix>.<last_octet>`.

### Temperature Thresholds
- **CHIP Temperature**:
  - E9 Pro: Maximum temperature can be specified via `--max_temp_e9` (default is 84°C).
  - L7: Maximum temperature can be specified via `--max_temp_l7` (default is 80°C).
- **PCB Temperature**: If the PCB temperature exceeds 70°C, an alert is sent.

### Hashrate Thresholds
- The script monitors both 5-second and 30-minute hash rates against predefined thresholds for each miner type. These values can be customized using the command-line arguments or configuration file.

## Using with Cron
To continuously monitor the miners, you can schedule the script to run periodically using cron.

### Setting Up a Cron Job
1. Make sure to use the full paths for Python and your script to avoid path issues.
2. Edit your cron jobs using:
   ```sh
   crontab -e
   ```
3. Add a line to run the script at the desired interval. For example, to run the script every 10 minutes:
   ```sh
   */10 * * * * /path/to/venv/bin/python /path/to/miner_check.py --config /path/to/config.json >> /path/to/logs/cron_output.log 2>&1
   ```
   This will execute the script every 10 minutes and log the output to `cron_output.log`.

## License
This project is licensed under the MIT License. See the LICENSE file for more details.

## Contributing
Contributions are welcome! If you have suggestions for improving the script, feel free to fork the repository, create an issue, or submit a pull request.

## Coffee
Tether USDT (ERC20) 0xcd53ffad3d2912cbc29288b3e961958e218864c3

