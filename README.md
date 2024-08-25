# ForticlientScript
you will connect automatic with enter otp
```
#!/bin/bash

# Set the VPN server address and username
VPN_SERVER="host:port"
VPN_USER="username"
PASSWORD="password"

# Your OTPAUTH URL
otpauth_url="otpauth://totp/username@domain:?issuer=&secret=&digits=6&algorithm=SHA1&period=30"

# Extract the secret using grep and sed
secret=$(echo "$otpauth_url" | grep -oP '(?<=secret=)[^&]*')

# Generate the OTP using oathtool
OTP=$(oathtool --totp -b "$secret")

# you will add trusted-cert if need
# Run the openfortivpn command with the provided credentials
openfortivpn $VPN_SERVER -u $VPN_USER --trusted-cert 0000000000000000 --password "$PASSWORD$OTP"
```
make sure run file by root use `sudo`
make sure file have permission extecuting
