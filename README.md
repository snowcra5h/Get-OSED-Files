# Get-OSED-Files
Serve files to and from OSED Windows Machine
---

## presetup steps
### set up PATH
1. [ ] if you don't have `~/.local/bin`  in your PATH you will need to add it.
	- `if you use zsh change .bashrc to .zshrc`
bash
```bash
snowcrash@hoory.fook.n.sheeit $ echo 'export PATH=~/.local/bin:$PATH' | tee -a ~/.bashrc

snowcrash@hoory.fook.n.sheeit $ source ~/.bashrc
```
zsh
```bash
snowcrash@hoory.fook.n.sheeit $ echo 'export PATH=~/.local/bin:$PATH' | tee -a ~/.zshrc

snowcrash@hoory.fook.n.sheeit $ source ~/.zshrc
```

### connect to OSED vpn
1. [ ] connect to the OSED vpn
```bash
snowcrash@hoory.fook.n.sheeit $ sudo openvpn snow.ovpn
```
3. [ ] connect to OSED windows VM
```shell
snowcrash@hoory.fook.n.sheeit $ xfreerdp /monitors:0 /multimon /u:Offsec /p:lab /v:192.168.***.***
```
---

## setup steps
### LOCAL YOUR KALI VM
1. [ ] make a directory to serve files to and from locally
```bash
snowcrash@hoory.fook.n.sheeit $ mkdir ~/osedfs
```
2. [ ] add a test file to download on the windows VM
```bash
snowcrash@hoory.fook.n.sheeit $ echo 'Hello.' > ~/osedfs/test.txt
```
3. [ ] install updog
```bash
snowcrash@hoory.fook.n.sheeit $ pip3 install updog
```
4. [ ] serve from directory you made in step one using port 9000 or what ever port you want
```bash
snowcrash@hoory.fook.n.sheeit $ updog -d ~/osedfs -p 9000
updog -d ~/osedfs -p 9000
[+] Serving /home/snowcrash/osedfs...
 * Running on all addresses (0.0.0.0)
 * Running on http://127.0.0.1:9000
 * Running on http://*********:9000
Press CTRL+C to quit
```
	- Note that you may want to use the --ssl flag here for some things.
### REMOTE ON THE WINDOWS BOX
#### DOWNLOADING TO WINDOWS BOX
1. [ ] open powershell
2. [ ] download the file
```powershell
Windows PowerShell
Copyright (C) Microsoft Corporation. All rights reserved.

PS C:\Users\Offsec> (New-Object Net.WebClient).DownloadFile("http://192.168.*.***:9000/test.txt", "test.txt")
```
3. [ ] confirm download
```powershell
PS C:\Users\Offsec> dir

    Directory: C:\Users\Offsec

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
...
...
-a----         9/5/2022  11:49 AM              7 test.txt

PS C:\Users\Offsec>
```

### UPLOADING TO THE WINDOWS BOX
1. [ ] Open a web-browser and upload your files.
2. [ ] Click 'chose your file'
3. [ ] Click 'upload'
