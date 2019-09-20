ansible-role-isdbg
==================

Install InstallShield Debugger on Windows machines.

Requirements
------------

You need to have one of the following requirements met as this ansible role does not include required files for InstallShield Debugger:

*   InstallShield installed on control machine;
*   or prepare following files in a folder (keeping the directory structure) for ansible use;
    *   `System/ISDbg.exe`
    *   `System/SciLexer.dll`
    *   (optional) `Program/0409/ISdbg.chm`
    *   (optional) `Program/0411/ISdbg.chm`
*   or provide a local path or remote URL to a zip containing files mentioned above where every file is put directly under the zip.
    *   `ISDbg.exe`
    *   `SciLexer.dll`
    *   (optional) `ISdbg.chm`

This ansible role runs on both Windows and Linux.

Role Variables
--------------

Variable        | Default  | Comment
--------------- | -------- | -------
ISVersion       | `"2019"` | The InstallShield Release
ISProductFolder | `C:\Program Files (x86)\InstallShield\2019` | Source Folder to Search on Control Machine
ISDbgZip        | (undefined) | Source zip which contains required files; <br>Specify this variable to skip searching on control machine.
ISDbgFolder     | `C:\ISDbg\2019` | Destination Folder to Install on Remote Machine

Dependencies
------------

None.

Example Playbook
----------------

*   Copy InstallShield debugger from local InstallShield installation on Windows:

    ```yaml
    #!/usr/bin/env ansible-playbook
    ---
    - hosts: isdbg
      gather_facts: no
      roles:
        - name: pallxk/isdbg
          ISVersion: "2019"
          ISProductFolder: C:\Program Files (x86)\InstallShield\2019
          ISDbgFolder: C:\ISDbg\{{ ISVersion }}
    ```

*   Copy InstallShield debugger from local InstallShield installation on Linux:

    ```yaml
    #!/usr/bin/env ansible-playbook
    ---
    - hosts: isdbg
      gather_facts: no
      roles:
        - name: pallxk/isdbg
          ISVersion: "2019"
          ISProductFolder: ~/InstallShield/2019
          ISDbgFolder: C:\ISDbg\{{ ISVersion }}
    ```

*   Copy InstallShield debugger from local zip file:

    ```yaml
    #!/usr/bin/env ansible-playbook
    ---
    - hosts: isdbg
      gather_facts: no
      roles:
        - name: pallxk/isdbg
          ISVersion: "2019"
          ISDbgZip: C:\Downloads\isdbg2019.zip
          ISDbgFolder: C:\ISDbg\{{ ISVersion }}
    ```

*   Copy InstallShield debugger from HTTP source:

    ```yaml
    #!/usr/bin/env ansible-playbook
    ---
    - hosts: isdbg
      gather_facts: no
      roles:
        - name: pallxk/isdbg
          ISVersion: "2019"
          ISDbgZip: "https://example.com/isdbg2019.zip"
          ISDbgFolder: C:\ISDbg\{{ ISVersion }}
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
