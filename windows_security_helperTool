@echo off
title Sistema de Verificacao Avancada - by Marcelo P
color 0E

:: ============================================
:: AVISO: Execute como ADMINISTRADOR
:: WARNING: Run as Administrator
:: ============================================

echo Criado por : Marcelo P
echo GitHub : https://github.com/MpasPrime
echo.
echo Iniciando verificacoes do sistema...
echo Starting system checks...
echo.

net session >nul 2>&1
if %errorlevel% neq 0 (
    echo Execute como ADMINISTRADOR! / Run as ADMINISTRATOR!
    pause
    exit
)

set output=%userprofile%\Desktop\relatorio_seguranca.txt
echo ===== SECURITY REPORT (EN) ===== > "%output%"

:: ============================================
:: AVISO: Encerramento de processos comuns usados por scripts maliciosos
:: WARNING: Stops common scripting processes used by malware
:: ============================================

echo [1] Encerrando processos suspeitos... / Stopping suspicious processes...
for %%p in (wscript.exe cscript.exe mshta.exe powershell.exe) do (
    taskkill /f /im %%p >nul 2>&1
)
echo Processes terminated successfully. >> "%output%"
echo.

:: ============================================
:: AVISO: Restaurar HOSTS remove redirecionamentos maliciosos
:: WARNING: Restoring HOSTS removes malicious redirects
:: ============================================

echo [2] Restaurando HOSTS... / Restoring HOSTS...
attrib -r -h -s C:\Windows\System32\drivers\etc\hosts
echo # Default Windows HOSTS > C:\Windows\System32\drivers\etc\hosts
echo 127.0.0.1 localhost >> C:\Windows\System32\drivers\etc\hosts
echo ::1 localhost >> C:\Windows\System32\drivers\etc\hosts
echo HOSTS restored successfully. >> "%output%"
echo.

:: ============================================
:: AVISO: Verificacao de disco pode exigir reinicio
:: WARNING: Disk check may require restart
:: ============================================

echo [3] Verificando disco... / Checking disk...
chkdsk C: /f /r
echo Disk verification completed. >> "%output%"
echo.

:: ============================================
:: AVISO: Verifica integridade dos arquivos do sistema
:: WARNING: Verifies system file integrity
:: ============================================

echo [4] Verificando sistema... / Scanning system files...
sfc /scannow
echo System integrity verification completed. >> "%output%"
echo.

:: ============================================
:: AVISO: Analise de persistencia (startup, tarefas e servicos)
:: WARNING: Persistence analysis (startup, tasks and services)
:: ============================================

echo [5] Analisando inicializacao e persistencia... / Checking startup and persistence...

echo ===== Startup Entries (EN) ===== >> "%output%"
reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Run >> "%output%" 2>nul
reg query HKLM\Software\Microsoft\Windows\CurrentVersion\Run >> "%output%" 2>nul

echo ===== Scheduled Tasks (EN) ===== >> "%output%"
schtasks /query /fo LIST /v >> "%output%" 2>nul

echo ===== Services (EN) ===== >> "%output%"
sc query type= service state= all >> "%output%" 2>nul

echo Persistence analysis completed. >> "%output%"
echo.

:: ============================================
:: AVISO: Heuristica baseada em local + atributo oculto + extensao
:: WARNING: Heuristic based on location + hidden attribute + extension
:: ============================================

echo [6] Analise heuristica... / Running heuristic scan...

set ext=*.exe *.bat *.cmd *.vbs *.js *.ps1
echo ===== Heuristic Findings (EN) ===== >> "%output%"

:: TEMP (remocao segura)
for %%e in (%ext%) do (
    for /f "delims=" %%f in ('dir C:\Windows\Temp\%%e /a:h /s /b 2^>nul') do (
        echo Suspicious file (TEMP): %%f >> "%output%"
        del /f /q "%%f"
    )
)

for %%e in (%ext%) do (
    for /f "delims=" %%f in ('dir %temp%\%%e /a:h /s /b 2^>nul') do (
        echo Suspicious file (USER TEMP): %%f >> "%output%"
        del /f /q "%%f"
    )
)

:: PUBLIC (remocao segura)
for %%e in (%ext%) do (
    for /f "delims=" %%f in ('dir C:\Users\Public\%%e /a:h /s /b 2^>nul') do (
        echo Suspicious file (PUBLIC): %%f >> "%output%"
        del /f /q "%%f"
    )
)

:: APPDATA (somente analise)
for %%e in (%ext%) do (
    for /f "delims=" %%f in ('dir %userprofile%\AppData\%%e /a:h /s /b 2^>nul') do (
        echo Suspicious file (APPDATA - review required): %%f >> "%output%"
    )
)

echo Heuristic scan completed. >> "%output%"
echo.

:: ============================================
:: AVISO: Verificacao de assinatura digital
:: WARNING: Digital signature verification
:: ============================================

echo [7] Verificando assinaturas digitais... / Checking digital signatures...

echo ===== Digital Signature Check (EN) ===== >> "%output%"

where sigcheck >nul 2>&1
if %errorlevel%==0 (
    echo Sigcheck detected. Running verification... >> "%output%"
    
    for %%f in (C:\Windows\System32\*.exe) do (
        sigcheck "%%f" -q -m >> "%output%" 2>nul
    )

    echo Digital signature verification completed. >> "%output%"
) else (
    echo Sigcheck not found. Skipping signature verification. >> "%output%"
    echo.
    echo AVISO: Sigcheck nao encontrado!
    echo WARNING: Sigcheck not found!
    echo.
    echo Baixe em:
    echo Download at:
    echo https://learn.microsoft.com/sysinternals/downloads/sigcheck
)

echo.

:: ============================================
:: RESUMO FINAL
:: ============================================

echo ===== RESUMO (PT-BR) ===== >> "%output%"
echo Processos suspeitos encerrados >> "%output%"
echo HOSTS restaurado >> "%output%"
echo Disco verificado >> "%output%"
echo Sistema verificado >> "%output%"
echo Persistencia analisada >> "%output%"
echo Arquivos suspeitos removidos (Temp/Public) >> "%output%"
echo AppData analisado com seguranca >> "%output%"
echo Assinaturas digitais verificadas ou ignoradas >> "%output%"

:: ============================================
:: FINAL
:: ============================================

color 0A
echo.
echo ===============================
echo Finalizando... / Finishing...
echo ===============================
echo Relatorio salvo em / Report saved at:
echo %output%

pause
