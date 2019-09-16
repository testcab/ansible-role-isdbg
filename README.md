ansible-role-isdbg
==================

Install InstallShield Debugger on Windows machines.

Requirements
------------

You need to have InstallShield installed on control machine, or prepare `System/ISDbg.exe`, `System/SciLexer.dll` and optionally `Program/0409/ISdbg.chm` or `Program/0411/ISdbg.chm` in a folder for ansible use. This ansible role does not include those required files.

This ansible role runs on both Windows and Linux.

Role Variables
--------------

Variable        | Default  | Comment
--------------- | -------- | -------
ISVersion       | `"2019"` | The InstallShield Release
ISProductFolder | `C:\Program Files (x86)\InstallShield\2019` | Source Folder to Search on Control Machine
ISDbgFolder     | `C:\ISDbg\2019` | Destination Folder to Install on Remote Machine

Dependencies
------------

None.

Example Playbook
----------------

```yaml
#!/usr/bin/env ansible-playbook
---
- hosts: isdbg
  gather_facts: no
  roles:
    - name: pallxk/isdbg
      ISVersion: "2019"
      ISProductFolder: ~/InstallShield/2019
      #ISProductFolder: C:\Program Files (x86)\InstallShield\2019
      #ISDbgFolder: C:\ISDbg\{{ ISVersion }}
```

License
-------

The MIT License (MIT)

Author Information
------------------

[pallxk](https://github.com/pallxk)
[testcab](https://github.com/testcab)


References
----------

* https://helpnet.flexerasoftware.com/installshield25helplib/installshield25helplib.htm#Subsystems/ISdbg/helplibrary/DebuggingInstall-AnyComputer.htm
* https://zzz.buzz/2018/06/25/installshield-installscript-project-remote-debugging/
