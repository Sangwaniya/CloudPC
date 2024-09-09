# Free CloudPC in 2 steps by GitHub workflow cloud
### Network Speed: 5GB per sec, i5 latest gen and 8 gb ram
1. Copy the github workflow file main.yaml
- .github/workflows/main.yaml
```yaml:
name: CI
on: [push, workflow_dispatch]
jobs:
  build:
    runs-on: windows-latest
    timeout-minutes: 360  # Set the timeout to 6 hours
    steps:
    - name: Download
      run: Invoke-WebRequest https://bin.equinox.io/c/bNyj1mQVY4c/ngrok-v3-stable-windows-amd64.zip -OutFile ngrok.zip
    - name: Extract
      run: Expand-Archive ngrok.zip
    - name: Auth
      run: .\ngrok\ngrok.exe authtoken $Env:NGROK_AUTH_TOKEN
      env:
        NGROK_AUTH_TOKEN: ${{ secrets.NGROK_AUTH_TOKEN }}
    - name: Enable TS
      run: Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server'-name "fDenyTSConnections" -Value 0
    - run: Enable-NetFirewallRule -DisplayGroup "Remote Desktop"
    - run: Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "UserAuthentication" -Value 1
    - run: Set-LocalUser -Name "runneradmin" -Password (ConvertTo-SecureString -AsPlainText "Pass@1234" -Force)
    - name: Create Tunnel
      run: .\ngrok\ngrok.exe tcp 3389
```
2. Set env variable value for NGROK_AUTH_TOKEN :
```
env:
  NGROK_AUTH_TOKEN: 'Your Authtoken Value'
```
 Your Authtoken you can get by sign in to ngrok website ->>Your Authtoken https://dashboard.ngrok.com/get-started/your-authtoken.
Now after merging the code, go to ngrok ->> cloudEdge ->> Endpoints 
Now here you found the endpoint to connect with RDP, using Windows remote desktop connection ![image](https://github.com/Sangwaniya/CloudPC/assets/87386688/a3a58dce-0b61-442c-ad7b-a47a213da4e4)

Credentials : 
username - runneradmin
password- Pass@1234

Enjoyyyyyyyyyyyy yourrrrrrr freeeeeee and secure RDPPPPPPP frommmmmmmmmm GitHubbbbbbbbbbbbb.
 
.github/workflows file
