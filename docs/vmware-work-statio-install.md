## Share folder

[Now, I will show you how to **share folder** between host and guest machine.][4]

![Imgur](https://i.imgur.com/2B74jZ4.png)

First of all you shoudl take a look this
```
Prerequisites
- Verify that the virtual machines use a guest operating system that supports shared folders.
See Guest Operating Systems that Support Shared Folders.
- Verify that the latest version of VMware Tools is installed in the guest operating system.
- Verify that permission settings on the host system allow access to files in the shared folders.
For example, if you are running Workstation as a user named User, the virtual machine can read and 
write files in the shared folder only if User has permission to read and write them.

```
## Procedure
1. Select the virtual machine and select VM > Settings.
2. On the Options tab, select Shared Folders.
3. Select a folder sharing option.

![Imgur](https://i.imgur.com/2wMJCOq.png)

Explain:

| Option        | Description                 |
|---------------|-----------------------------|
| Always enabled | Keep folder sharing enabled, even when the virtual machine is shut down, suspended, or powered off. |
| Enabled until next power off or suspend| Enable folder sharing temporarily, until you power off, suspend, or shut down the virtual machine. If you restart the virtual machine, shared folders remain enabled. This setting is available only when the virtual machine is powered on.|

4. (Optional) To map a drive to the Shared Folders directory, select **Map as a network drive in Windows guests**.
This directory contains all of the shared folders that you enable. Workstation selects the drive letter.

5. Click **Add** to add a shared folder.
On Windows hosts, the Add Shared Folder wizard starts. On Linux hosts, the Shared Folder Properties dialog box opens.

![Imgur](https://i.imgur.com/rqlBXJO.png)

6. Type the path on the host system to the directory to share.
If you specify a directory on a network share, such as **D:\share**, Workstation always attempts to use that path.
If the directory is later connected to the host on a different drive letter, Workstation cannot locate the shared folder.

7. Specify the name of the shared folder as it should appear inside the virtual machine.
Characters that the guest operating system considers illegal in a share name appear differently when viewed inside the guest.
For example, if you use an asterisk in a share name, you see %002A instead of * in the share name on the guest. 
Illegal characters are converted to their ASCII hexadecimal value

![Imgur](https://i.imgur.com/tmlFu5Q.png)

8. Select shared folder attributes.

| Option  | Description |
|---------|-------------|
|Enable this share| Enable the shared folder. Deselect this option to disable a shared folder without deleting it from the virtual machine configuration.|
|Read-only| Make the shared folder read-only. When this property is selected, the virtual machine can view and copy files from the shared folder, but it cannot add, change, or remove files. Access to files in the shared folder is also governed by permission settings on the host computer.|

9. Click Finish to add the shared folder.
![Imgur](https://i.imgur.com/kKsy8db.png)
The shared folder appears in the Folders list. The check box next to folder name indicates that the folder is being shared. 
You can deselect this check box to disable sharing for the folder.

10. Click **Save** to save your changes.

And then you can open your virtual machine, see it!!!
![Imgur](https://i.imgur.com/6VdLXNa.png)

## Rerfences

[4]: https://pubs.vmware.com/workstation-9/index.jsp?topic=%2Fcom.vmware.ws.using.doc%2FGUID-D6D9A5FD-7F5F-4C95-AFAB-EDE9335F5562.html
