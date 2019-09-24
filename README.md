ansible-role-isdbg
==================

Install InstallShield Debugger onto Windows machines.

Requirements
------------

You need to have one of the following requirements met as this ansible role does not include required files for InstallShield Debugger:

*   Prepare following files in a folder (keeping the directory structure) for ansible use;
    *   `System/ISDbg.exe`
    *   `System/SciLexer.dll`
    *   (optional) `Program/0409/ISdbg.chm`
    *   (optional) `Program/0411/ISdbg.chm`
*   or provide a local path or remote URL to a zip containing files mentioned above where every file is put directly under the zip;
    *   `ISDbg.exe`
    *   `SciLexer.dll`
    *   (optional) `ISdbg.chm`
*   or InstallShield installed on control node. Note that to run this ansible role from Windows machine, you will need Cygwin and ansible installed within it.

Role Variables
--------------

Variable        | Default                    | Comment
--------------- | -------------------------- | -------
ISVersion       | (undefined)                | The InstallShield Release
ISProductFolder | (undefined)                | Source folder to search on control node;  <br>One of `ISProductFolder` and `ISDbgZip` must be specified.
ISDbgZip        | (undefined)                | Source zip which contains required files; <br>One of `ISProductFolder` and `ISDbgZip` must be specified.
ISDbgFolder     | `C:\ISDbg\{{ ISVersion }}` | Destination Folder to Install on Remote Machine

Dependencies
------------

None.

Example Playbook
----------------

*   Copy InstallShield debugger from local InstallShield installation on Linux:

    ```yaml
    #!/usr/bin/env ansible-playbook
    ---
    - hosts: isdbg
      gather_facts: no
      roles:
        - name: pallxk/isdbg
          ISVersion: "2019"
          ISProductFolder: ~/Downloads/ISDbg/2019
          ISDbgFolder: C:\ISDbg\{{ ISVersion }}
    ```

*   Copy InstallShield debugger from local InstallShield installation on Windows Cygwin:

    ```yaml
    #!/usr/bin/env ansible-playbook
    ---
    - hosts: isdbg
      gather_facts: no
      roles:
        - name: pallxk/isdbg
          ISVersion: "2019"
          ISProductFolder: /cygdrive/c/Program Files (x86)/InstallShield/2019
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
          ISDbgZip: ~/Downloads/isdbg2019.zip
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
