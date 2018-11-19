

`winrs -r:http://localhost:5985/wsman -u:ra\winrm-user -p:winrm ipconfig`

What is WinRM?
WinRM is a management protocol used by Windows to remotely communicate with another server. It is a SOAP-based protocol that communicates over HTTP/HTTPS, and is included in all recent Windows operating systems. Since Windows Server 2012, WinRM has been enabled by default, but in most cases extra configuration is required to use WinRM with Ansible.
