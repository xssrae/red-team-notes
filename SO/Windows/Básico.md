---
tags:
  - Windows
  - SO
---
# Listar processos
```powershell
Get-CimInstance -ClassName win32_service | Select Name,State,PathName,StartName | Where-Object {$_.State -like 'Running'}
```

# Kill
```powershell
# Lista todos os processos que estão rodando 
netstat -ano 
# Lista todos os processos que estão rodando na porta 8000 
netstat -ano | findstr 8000 
# Mata processo que está rodando na porta 8000 pelo PID 
taskkill /f /pid <PID>
```

