# imageinfo

- Profile - Win7SP1x86\_23418

# pstree

- jackal.exe.exe - pid 3028
	- cmd.exe - pid 1084
	- cmd.exe - pid 1608 (terminated)

# 1084
## strings
### procdump
Registrys mentioned
```
SOFTWARE\POLICIES\MICROSOFT\WINDOWS\SYSTEM
SOFTWARE\MICROSOFT\COMMAND PROCESSOR
SOFTWARE\CLASSES
```

## handles -t file
```
\Device\HarddiskVoIume1\Users\Daniel
\Device\HarddiskVoIume1\Windows\System32 -US\cmd.exe.mui
\Device\Afd\Endpoint
\Device\Afd\Endpoint
\Device\Afd\Endpoint
```

## handles -t key
```
MACHINE\SYSTEM\CONTROLSET001\CONTROL\NLS\SORTING\VERSIONS                                                                                                                                                          
MACHINE\SYSTEM\CONTROLSET001\CONTROL\SESSION                                                                                                                                                                       
MACHINE                                                                                                                                                                                                            
USER\S-1-5-21-2833823845-3085568943-3082117713-1000                                                                                                                                                                
MACHINE\SYSTEM\CONTROLSET001\CONTROL\NLS\LOCALE                                                                                                                                                                    
MACHINE\SYSTEM\CONTROLSET001\CONTROL\NLS\LOCALE\ALTERNATE                                                                                                                                                          
MACHINE\SYSTEM\CONTROLSET001\CONTROL\NLS\LANGUAGE
```

# 3028
## handles -t file
```
\Device\Harddiskvolume1\Users\Daniel
\Device\HarddiskVolume1\Users\Daniel\AppData\Local\Microsoft\Windows\Temporary Internet Files\Content.IE5\index.dat
\Device\HarddiskVolume1\Users\Daniel\AppData\Windows\Cookies\index.dat
\Device\HarddiskVolume1\Users\Daniel\AppData\Local\Microsoft\Windows\History\History.IE5\index.dat
\Device\HarddiskV01ume1\Windows\winsxs\x86_microsoft.windows.common-controls_6595b64144ccf1df 6.0.7601.17514_none_41e6975e2bd6f2b2
\Device\Afd\Endpoint
\Device\KsecDD
\Device\Afd\Endpoint
\Device\Nsi
\Device\Afd\AsyncConnectHlp
\Device\Afd\Endpoint
```

## handles -t key
```
MACHINE\SYSTEM\CONTROLSET001\CONTROL\NLS\SORTING\VERSIONS                                                                                                                                                      
MACHINE                                                                                                                                                                                                            
MACHINE\SYSTEM\CONTROLSET001\CONTROL\SESSION                                                                                                                                                                       
USER\S-1-5-21-2833823845-3085568943-3082117713-1000                                                                                                                                                                
USER\S-1-5-21-2833823845-3085568943-3082117713-1000\SOFTWARE\MICROSOFT\WINDOWS                                                                                                                                     
USER\S-1-5-21-2833823845-3085568943-3082117713-1000\SOFTWARE\MICROSOFT\WINDOWS\CURRENTVERSION\INTERNET                                                                                                             
USER\S-1-5-21-2833823845-3085568943-3082117713-1000\SOFTWARE\MICROSOFT\WINDOWS\CURRENTVERSION\EXPLORER                                                                                                             
USER\S-1-5-21-2833823845-3085568943-3082117713-1000\SOFTWARE\POLICIES\MICROSOFT\WINDOWS\CURRENTVERSION\INTERNET                                                                                                    
MACHINE\SOFTWARE\POLICIES\MICROSOFT\WINDOWS\CURRENTVERSION\INTERNET                                                                                                                                                
USER\S-1-5-21-2833823845-3085568943-3082117713-1000\SOFTWARE\MICROSOFT\WINDOWS\CURRENTVERSION\INTERNET                                                                                                             
MACHINE\SOFTWARE\POLICIES                                                                                                                                                                                          
USER\S-1-5-21-2833823845-3085568943-3082117713-1000\SOFTWARE\POLICIES                                                                                                                                              
USER\S-1-5-21-2833823845-3085568943-3082117713-1000\SOFTWARE                                                                                                                                                       
MACHINE\SOFTWARE                                                                                                                                                                                                   
MACHINE\SOFTWARE\MICROSOFT\WINDOWS\CURRENTVERSION\INTERNET                                                                                                                                                         
MACHINE\SYSTEM\CONTROLSET001\SERVICES\WINSOCK2\PARAMETERS\PROTOCOL_CATALOG9                                                                                                                                        
MACHINE\SYSTEM\CONTROLSET001\SERVICES\WINSOCK2\PARAMETERS\NAMESPACE_CATALOG5                                                                                                                                       
USER\S-1-5-21-2833823845-3085568943-3082117713-1000\SOFTWARE\MICROSOFT\INTERNET                                                                                                                                    
MACHINE\SOFTWARE\MICROSOFT\INTERNET                                                                                                                                                                                
USER\S-1-5-21-2833823845-3085568943-3082117713-1000_CLASSES                                                                                                                                                        
USER                                                                                                                                                                                                               
USER\S-1-5-21-2833823845-3085568943-3082117713-1000                                                                                                                                                                
MACHINE\SOFTWARE\MICROSOFT\TRACING\JACKAL_RASAPI32                                                                                                                                                                 
MACHINE\SOFTWARE\MICROSOFT\TRACING\JACKAL_RASMANCS                                                                                                                                                                 
USER\S-1-5-21-2833823845-3085568943-3082117713-1000\SOFTWARE\MICROSOFT\WINDOWS\CURRENTVERSION\INTERNET                                                                                                             
USER\S-1-5-21-2833823845-3085568943-3082117713-1000\SOFTWARE\MICROSOFT\WINDOWS                                                                                                                                     
MACHINE\SOFTWARE\MICROSOFT\WINDOWS                                                                                                                                                                                 
MACHINE\SOFTWARE\MICROSOFT\WINDOWS                                                                                                                                                                                 
USER\S-1-5-21-2833823845-3085568943-3082117713-1000\SOFTWARE\MICROSOFT\WINDOWS                                                                                                                                     
MACHINE\SOFTWARE\MICROSOFT\WINDOWS\CURRENTVERSION\INTERNET                                                                                                                                                         
MACHINE\SOFTWARE\MICROSOFT\INTERNET                                                                                                                                                                                
MACHINE\SOFTWARE\MICROSOFT\INTERNET
```