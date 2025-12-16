# Setting Up File Sharing in the Active Directory Environment
I configured a file server within the domain to provide centralized file access using Active Directory users and security groups.

#### Steps I Performed

1. On the domain controller, I created a folder (SHARED) on a dedicated drive.
2. I right-clicked the folder → Properties → Sharing → Advanced Sharing.
    * Enabled Share this folder
    * Assigned a share name (Users)
    <img width="1920" height="1036" alt="image" src="https://github.com/user-attachments/assets/003e34d3-ba07-46d4-b19a-ce307b2f819e" />
3. I configured Share Permissions to allow access only to the appropriate security groups (e.g. HR_Staff, IT_Staff).
    <img width="1920" height="1037" alt="image" src="https://github.com/user-attachments/assets/d4a2f675-b9b8-4375-b7b5-91521b4b10f9" />

4. On the Windows 11 client, I accessed the share using the Map Network Drive method.
   \\Server\SHARED
   Access was granted based on the user’s group membership, confirming permissions were applied correctly.
    <img width="1920" height="1035" alt="image" src="https://github.com/user-attachments/assets/cae3bac7-c84e-4da2-a2a8-302c2b8e3316" />
    
5. The Map Network Drive method isn't consistent because When I restart my PC, I have to Map the Network Drive over again. in other to make it easily accessible, I             configured a GPO to automatically map network drives for users.
   * Create a new GPO under the Group Policy Object, name it Mapped Drive
   * Edit the Mapped Drive,
     User Configuration → Preferences → Windows Settings → Drive Maps
     <img width="1920" height="1040" alt="image" src="https://github.com/user-attachments/assets/42ee23e4-1858-40b5-832c-53584664ebeb" />
   * I Linked the Map Drive to the right OU (USA) and assign the GPO to the Users.

6.  On the Windows 11 client, I accessed the SHARED (S) folder successfully.
     <img width="1920" height="1037" alt="image" src="https://github.com/user-attachments/assets/8fe6de51-6c06-4728-8ba0-3e057c7af3dc" />

   




Why This Matters
This demonstrates my understanding of centralized file management, role-based access control, and the difference between Share permissions and NTFS permissions in an Active Directory environment.
