# 10linesNoRevoke
10行代码防回撤，10行脚本代码把pc微信变防撤回（仅支持微信版本3.9.0.28！！！）
## 使用方法：
在退出微信进程的时候执行本脚本即可（登录界面也要退出）  
把10行代码复制到打开的powershell执行即可  
```PowerShell
$temp = (Get-ItemProperty "HKCU:\SOFTWARE\tencent\wechat").installpath
$binaryFile = Get-ChildItem -Path $temp -Recurse -Include wechatwin.dll | Select-Object -ExpandProperty FullName
echo $binaryFile
Get-FileHash -LiteralPath $binaryFile
$bytes  = [System.IO.File]::ReadAllBytes($binaryFile)
$offset1= 0x00B4B3EA
$offset2= 0x00B4B419
$bytes[$offset1]=0xeb
$bytes[$offset2]=0
[System.IO.File]::WriteAllBytes($binaryFile, $bytes)
Get-FileHash -LiteralPath $binaryFile
```

      

## 执行成功的话，会有下面的2个值
![image](https://user-images.githubusercontent.com/50006539/225555345-4896efa0-d24f-42e4-9fa2-e0ac52c5e687.png)
