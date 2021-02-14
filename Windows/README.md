Windows
===


##### [regedit](https://zh.wikipedia.org/wiki/%E6%B3%A8%E5%86%8C%E8%A1%A8)
```
電腦->連線網路磁碟機->資料夾    HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Map Network Drive MRU
```
##### [services.msc](https://zh.wikipedia.org/wiki/%E6%9C%8D%E5%8A%A1%E6%8E%A7%E5%88%B6%E7%AE%A1%E7%90%86%E5%99%A8)
---

##### Enable Telnet Server
```
> net localgroup TelnetClients /add
> net localgroup TelnetClients VAST-Server /add
> net localgroup TelnetClients

Change Telnet Server Auth
> tlntadmn config sec -ntlm passwd
> tlntadmn
```
##### Windows 7 Default Dir Path is "MY Computer"
```
%WINDIR%\explorer.exe ::{20D04FE0-3AEA-1069-A2D8-08002B30309D} ， ::{20D04FE0-3AEA-1069-A2D8-08002B30309D}
```
---

##### chcp 65001
##### systeminfo /?    此工具可顯示本機或遠端機器的作業系統設定資訊，包括 Service Pack 等級。
##### ipconfig /?
```
> ipconfig /all
> ipconfig /displaydns
> ipconfig /flushdns
```
##### ping /?
```
> ping <IP> -f -l <MTU Size>
```
##### net /?
```
> net use

> net use <磁碟機代號>: \\<IP or HostName>\<資料夾名稱> /user:<Domain>\<Account> <Password>
> net use z: \\192.168.1.xxx\myFiles /user:Domain\Administrator 123
> net use z: \\192.168.1.xxx\myFiles /user:Domain\Administrator ""
> net use z: /delete
```
##### xcopy /?
```
> xcopy C:\xxx F:\xxx /s
  C:\xxx 為複製檔案來源位置: 例如要複製整個C槽就輸入C:\
  F:\xxx 為複製目的位置: 例如要放到F槽的備份資料夾就輸入F:\備份
  /s     為複製類型參數: 複製每個目錄及其包含的子目錄但不複製空目錄
```
##### netsh /?
```
> netsh interface show interface
> netsh winsock reset

> netsh interface ipv4 set address "Ethernet 2" source=dhcp
> netsh interface ipv4 set dnsservers name="Ethernet 2" source=dhcp
> netsh interface ipv4 set winsservers name="Ethernet 2" source=dhcp
```
##### netstat /?    顯示通訊協定統計資料和目前的 TCP/IP 網路連線。
##### route/?    操控網路路由表
```
> route -p add 10.0.0.0 mask 255.0.0.0 192.168.0.1 metric 30 if 2
```
##### tasklist /?    此工具會顯示本機或遠端電腦上，目前正在執行中的處理程序清單。
##### taskkill /?    此工具可用於依據處理程序識別碼 (PID) 或影像名稱來終止工作。
##### schtasks/?    讓系統管理員能夠在建立、刪除、查詢、變更，和執行，結束排程工作。
```
> schtasks /create /f /tn "TaskName" /tr "dir" /sc onstart
> schtasks /run /tn "TaskName"
> schtasks /end /tn "TaskName"
> schtasks /delete /tn "TaskName" /f
```
##### type /?    顯示文字檔案的內容。
##### del /?    刪除一個或多個檔案。
```
> del /s /ah Thumbs.db
```
##### rd /?    移除 (刪除) 一個目錄。
```
清理資源回收筒指令
> rd /s /q %systemdrive%\$Recycle.bin
```
---

###### 檔案總管從「本機」中移除「NameSpace」.reg
```
Windows 10 檔案總管->從「本機」中移除「NameSpace」

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\MyComputer\NameSpace
HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Explorer\MyComputer\NameSpace

從「本機」中移除「Desktop」      {B4BFCC3A-DB2C-424C-B029-7FE99A87C641}
從「本機」中移除「Downloads」    {374DE290-123F-4565-9164-39C4925E467B}  {088e3905-0323-4b02-9826-5d99428e115f}
從「本機」中移除「文件」         {A8CDFF1C-4878-43be-B5FD-F8091C1C60D0}  {d3162b92-9365-467a-956b-92703aca08af}
從「本機」中移除「音樂」         {1CF1260C-4DD0-4ebb-811F-33C572699FDE}  {3dfdf296-dbec-4fb4-81d1-6a3438bcf4de}
從「本機」中移除「圖片」         {3ADD1653-EB32-4cb0-BBD7-DFA0ABB5ACCA}  {24ad3ad4-a569-4530-98e1-ab02f9417aa8}
從「本機」中移除「影片」         {A0953C92-50DC-43bf-BE83-3742FED03C9C}  {f86fa3ab-70d2-4fc7-9c99-fcbf05467f3a}
從「本機」中移除「3D 物件」      {0DB7E03F-FC29-4DC6-9020-FF41B59E513A}
```
##### connectToSambaFromWindows10.reg
```
Windows 10 Connect to Linux Samba

HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\AllowInsecureGuestAuth=dword:00000001
```
---

##### macshift.exe: Macshift v2.0, MAC Changing Utility
```
> macshift.exe -i NIC1 000c29fff701
```
---
