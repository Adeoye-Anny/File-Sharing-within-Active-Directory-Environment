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
    
5. Manually mapping network drives is not persistent, as the connection may be lost after a system restart. To ensure consistent and automatic access to shared resources, I    configured a Group Policy Object (GPO) to map network drives for users at logon.

   * I created a new GPO named Mapped Drive under Group Policy Objects and edited it using the following path:
   * User Configuration → Preferences → Windows Settings → Drive Maps
     <img width="1920" height="1040" alt="image" src="https://github.com/user-attachments/assets/42ee23e4-1858-40b5-832c-53584664ebeb" />
   * This configuration automatically maps the required network drive each time a user signs in, ensuring reliable and centralized access across the domain.

6.  On the Windows 11 client, I accessed the SHARED (S) folder successfully.
     <img width="1920" height="1037" alt="image" src="https://github.com/user-attachments/assets/8fe6de51-6c06-4728-8ba0-3e057c7af3dc" />

#### Why This Matters
This demonstrates my understanding of centralized file management, role-based access control, and the difference between Share permissions and NTFS permissions in an Active Directory environment.



# Configuring File Server Resource Manager (FSRM)
I configured File Server Resource Manager (FSRM) to control disk usage and restrict unwanted file types. This helps prevent storage abuse and enforces proper file usage within the Active Directory environment.

### 1. Installing File Server Resource Manager
   1. I opened Server Manager → Manage → Add Roles and Features.
   2. I selected Role-based or feature-based installation.
   3. Under File and Storage Services → File and iSCSI Services, I selected File Server Resource Manager.
   4. I completed the installation successfully.
      <img width="1920" height="1037" alt="image" src="https://github.com/user-attachments/assets/e1e8da63-5d49-40af-bb53-b3baabcb7203" />


### 2. Creating a Quota Template
Purpose
Quota templates limit how much storage users or folders can consume.

#### Steps Performed
   1. I opened Server Manager → Tools → File Server Resource Manager.
   2. I navigated to Quota Management → Quota Templates.
   3. I created a new template:
      * Template name: Standard User Quota
      * Limit: 10 GB
      * Quota type: Hard quota
   4. I enabled notifications to alert administrators when 80% usage thresholds are reached.
      <img width="1920" height="1038" alt="image" src="https://github.com/user-attachments/assets/d02c4e69-5323-44c4-a332-fdcdc6c85ad7" />



### 3. Applying the Quota Template
   1. Under Quota Management, I selected Create Quota.
   2. I chose the target shared folder (S:\SHARED).
   3. I applied the Standard User Quota template.
      This immediately enforced storage limits on the folder.
      <img width="1920" height="1039" alt="image" src="https://github.com/user-attachments/assets/d13ee02c-91e8-4fcf-802d-4e7bc81bedef" />


### 4. Creating a File Screen Template
Purpose
File screen templates prevent users from storing unauthorized file types such as videos or executables.

#### Steps Performed
   1. In FSRM, I navigated to File Screening Management → File Screen Templates.
   2. I created a new template:
      Template name: SHARED
   3. Screening type: Active screening
   4. Blocked file groups: Audio and Video Files
   5. I enabled notifications for policy violations.
      <img width="1920" height="1038" alt="image" src="https://github.com/user-attachments/assets/a86215f3-b40d-4b98-b2b8-862e50be2ceb" />


5. Applying and Testing File Screening
   I applied the file screen template to the shared user folder.
   From a domain-joined Windows 11 client, I attempted to upload a blocked file type.
   The action was denied, confirming the policy was enforced correctly.



## Result
This configuration demonstrates my ability to:
   1. Control disk usage using quota templates
   2. Prevent unauthorized file storage
   3. Enforce centralized storage policies
   4. Manage file servers in an Active Directory environment




