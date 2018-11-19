

`winrs -r:http://localhost:5985/wsman -u:ra\winrm-user -p:winrm ipconfig`

What is WinRM?
WinRM is a management protocol used by Windows to remotely communicate with another server. It is a SOAP-based protocol that communicates over HTTP/HTTPS, and is included in all recent Windows operating systems. Since Windows Server 2012, WinRM has been enabled by default, but in most cases extra configuration is required to use WinRM with Ansible.

In Debian
`apt install python-pip`

Ansible uses the pywinrm package to communicate with Windows servers over WinRM. It is not installed by default with the Ansible package, but can be installed by running the following:

`pip install "pywinrm>=0.3.0"`

--- Create local user and add to Administrators groups

Basic
Basic authentication is one of the simplest authentication options to use, but is also the most insecure. This is because the username and password are simply base64 encoded, and if a secure channel is not in use (eg, HTTPS) then it can be decoded by anyone. Basic authentication can only be used for local accounts (not domain accounts).

The following example shows host vars configured for basic authentication:

--- in hosts use '='

ansible_user: LocalUsername
ansible_password: Password
ansible_connection: winrm
ansible_winrm_transport: basic


Basic authentication is not enabled by default on a Windows host but can be enabled by running the following in PowerShell:
Set-Item -Path WSMan:\localhost\Service\Auth\Basic -Value $true


ansible_winrm_server_cert_validation: Specify the server certificate validation mode (ignore or validate). Ansible defaults to validate on Python 2.7.9 and higher, which will result in certificate validation errors against the Windows self-signed certificates. Unless verifiable certificates have been configured on the WinRM listeners, this should be set to ignore

--

Non-Administrator Accounts
WinRM is configured by default to only allow connections from accounts in the local Administrators group. This can be changed by running:

winrm configSDDL default
This will display an ACL editor, where new users or groups may be added. To run commands over WinRM, users and groups must have at least the Read and Execute permissions enabled.

While non-administrative accounts can be used with WinRM, most typical server administration tasks require some level of administrative access, so the utility is usually limited.

--
