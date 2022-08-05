Lockdown has been around for a while, at least officially documented since SAS 9.4M1.  LOCKDOWN secures a SAS Foundation server by restricting access from within a server process to the host operating system.

1. It shuts down any SAS language feature that provides direct or indirect access to the operating system shell. This includes PROC GROOVY, and the DATA step Java Object and others. You also need to make sure that NOXCMD (shell command integration) and NORLANG (R language integration) are in place, since those avenues would circumvent any SAS-enforced system access.
2. It allows file access to only those directories that a SAS admin adds to a “whitelist”. This is the key benefit, since it prevents users from assigning arbitrary file-based libraries.

To allow specific file directory locations on a server, the following configuration changes should be made:

1. Create a new file and add the paths you wish to whitelist from LOCKDOWN.

<details><summary>/opt/sas/[tenant]/config/etc/lockdown/whitelist.txt</summary>
	/home
    /tmp
	/sso/data
	/sso/project
	/sastemp
    /opt/sas/spre/home/share/refdata/qkb
</details>

2. Edit the compsrv and workspaceserver `autoexec_usermods.sas` file:
 
- /opt/sas/[tenant]/config/etc/compsrv/default/autoexec_usermods.sas
- /opt/sas/[tenant]/config/etc/workspaceserver/default/autoexec_usermods.sas

```
filename lkdn “/opt/sas/[tenant]/config/etc/lockdown/whitelist.txt”; 
lockdown file=lkdn; 
```

3. Restart the spawner and runlauncher services.

```
systemctl restart sas-data-spawner-default.service
systemctl restart sas-data-runlauncher-default.service
```