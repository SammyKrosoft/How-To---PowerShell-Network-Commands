# Some Network Powershell commands

## Test-NetConnection

```powershell
Test-NetConnection -ComputerName Server001 -Port 443

TNC -ComputerName Server001 -Port 443
```

- Notes:
   - TCP test only
   - Has both ICMP (Ping) test and TCP test:
       - ICMP based ```PingSucceeded``` will return ```False``` if ICMP is deactivated on remote computer
       - ```TcPTestSucceeded``` property can still return ```True``` if ICMP is disabled on remote computer, it will show that the remote computer is listening on the specified port (and the port is opened outbound on the local machine)
   - Takes time as it waits for the Ping
   - Can use a predefined set of "common ports" using the following parameter: ```[-CommonTCPPort] {HTTP | RDP | SMB | WINRM}```
   - PowerShell Alias: TNC

Without parameters, the command will check if the computer is connected to Internet by testing Microsoft's ```internetbeacon.msedge.net``` host.

Use ```Test-NetConnection | fl *``` to display more information (DNS results, remote port, route, etc...)

> NOTE: There is a ```-InformationLevel Detailed``` parameter, there is a difference in the output if used without ```| format-list *``` but I didn't see any differences when using the *Format-List-wildcard* parameter :shrug:

![image](https://github.com/SammyKrosoft/How-To---PowerShell-Network-Commands/assets/33433229/67508d5c-f151-44b4-be2e-2d64eee7a8bc)

## Using System.Net.Sockets.TcpClient

```powershell
$ipaddress = IP_Address_Server 
$port = port 
$connection = New-Object System.Net.Sockets.TcpClient($ipaddress, $port)
if ($connection.Connected) {
     Write-Host "Success" 
} else { 
     Write-Host "Failed" 
}
```
