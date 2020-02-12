# Section III: Identity Access Management & S3 



### 1. IAM

In **Security, Identity & Compliance > IAM**

<img src="D:\Projectes\Curso_AWS_Architect\Section III Identity Acces Manag & S3\imgs\img1.PNG" width="600px" />

- Sign-in link: made up by your account number (sent to users). Changing it is a **DNS (Domain Name System)** change
- Customize: Account Alias: it's a **universal namespace** (si el nom ja esta pillat no es pot)



#### Security Status

##### Global

The region is Global inside all IAM. When we do such operations **we are not creating a particular user in N. Virginia** for instance, and then having to create it for Australia...

##### Dashboard (5/5)

###### Activate MultiFactor Authentication MFA

- Root account is the eamil address you use for AWS to sign-in
- When you log in using your **root acount** you are in the **God Mode**
- You don't want everyone to be loging in using the root account, we want to create users, groups and secure the groups... Enable MFA auth. so that if we get stolen the password they won't be able to access the account withouth the MFA.

<img src="D:\Projectes\Curso_AWS_Architect\Section III Identity Acces Manag & S3\imgs\img2.PNG" width="600px" />

<img src="D:\Projectes\Curso_AWS_Architect\Section III Identity Acces Manag & S3\imgs\img3.PNG" width="600px" />

- With Virtual MFA device: you download the Google Auth. app on the Google Play store or Apple App Store typing **Google Authenticator**. Open the app, hit the + button and scan the QR code. You need to wait until 2 MFA codes have been generated:

<img src="D:\Projectes\Curso_AWS_Architect\Section III Identity Acces Manag & S3\imgs\img4.PNG" width="600px" />

- **Show QR code**: take a picture of the QR and store it somewhere else (not the device you have downloaded the Google Authetincator App). It's for emergency cases when you lose your Virtual MFA device.  



###### Create Individual IAM user (Add a User)

- **Manage user > Add user** 
  - Set user name
  - Access type
    - **Programmatic access**
      - Used for the EC2 (virtual machine)
      - You create an access key ID and secret access key to interact with AWSC.
      - Used for the AWS API, CLI, SDK and other dev tools
    - **AWS Management Console access**
  - Permissions
    - Add user to group

<img src="D:\Projectes\Curso_AWS_Architect\Section III Identity Acces Manag & S3\imgs\img5.PNG" width="600px" />

This is for our programmatinc access to AWS (download the .csv) or send email to email the logging instructions.

###### Apply an IAM password policy

**Manage Password Policy**:

- Requirements of password policy (lowercase, expiration, reuse...)






##### Groups

- Select group name and attach policy:
  - **Job functions**:
    - AdministratorAccess (it's a Manage policty - orange box)
    - Billing
    - DatabaseAdministrator

##### Policies

- JSON notation

<img src="D:\Projectes\Curso_AWS_Architect\Section III Identity Acces Manag & S3\imgs\img6.PNG" width="600px" />

**Allow anything on any resource**: this is the most powerful policy that you can have on AWS



##### Users
- **Access Key ID**: is like a user name that we are going to use to programmatically access AWSC
- **Secret access key**: like a password to access AWSC
- **Consloe login link**: all we need to do is send your user, this console link and password.

**Users > Summary > Security Credentials **: 

- On Manage Console Access we can create a custom password or autogenerate a new one or disable the console...
- If you lost your access keys, in Access keys you can **Make inactive**

##### Roles

- A way an AWS service can go ahead and use another AWS service
- We will use it in the EC2 section when we are going to allow a VM to talk to S3
- **Create Role**:
  - Service: EC2, Lambda...
  - Look for Policies of S3 (if you want to have access to S3 from EC2)
  - **Role name**: unique name
  - The create roles appear in the table of the section **Roles**



### Summary - 1.IAM

- IAM is universal. Does not apply to regions
- The root account is the account created when you setup your AWS account for the 1st time. Complete Admin access.
- New users have **no permissions** when first created
- New users are assigned **Access Key ID & Secret Access Keys** when created
- **Such credentials are NOT the same as the password**. You cannot use the Access Key ID & Secret Access Key to Login in to the **console**, but you can use it to access **AWS via API and CLI**.
- If you lose them, you have to **regenerate them**.
- Setup a MFA on your root account **ALWAYS** (one can get all your passwords)
  - You need a device and Google Auth. App
- Create and customise your own password rotation policies. 





## 2. Billing Alarm

- Set the region to your working region.

- **Management and Governance** > **CloudWatch**: way of monitoring your cloud account.

- > **Billing** > Create an Alarm

<img src="D:\Projectes\Curso_AWS_Architect\Section III Identity Acces Manag & S3\imgs\img7.PNG" width="600px" />

<img src="D:\Projectes\Curso_AWS_Architect\Section III Identity Acces Manag & S3\imgs\img8.PNG" width="600px" />



### SNS Topic - Simple Notification Service - 

- Create a new Topic
- Enter the **email** where you will receive the notification
-  You have to go to the email and subscribe to the topic

<img src="D:\Projectes\Curso_AWS_Architect\Section III Identity Acces Manag & S3\imgs\img9.PNG" width="600px" />

<img src="D:\Projectes\Curso_AWS_Architect\Section III Identity Acces Manag & S3\imgs\img10.PNG" width="600px" />

## 3. Create S3 Bucket

Select N.Virginina cause is the first region that all the products were implemented, so selecting another region may imply that this product is not in the products for that region.

- When you create a Bucket you will **select the region where it will be**

- But when you go to **Buckets** you switch to a **Global** view

- Name of the Bucket name must be unique (DNS-compliant)

- Create Bucket:

  - Once created Upload a file and receive a HTTP Code 200 that the upload was successfull

  <img src="D:\Projectes\Curso_AWS_Architect\Section III Identity Acces Manag & S3\imgs\img11.PNG" height="500px" />

- If we click the **Object URL** you will find an XML access denied, cause we haven't make this **object PUBLIC**:

<img src="D:\Projectes\Curso_AWS_Architect\Section III Identity Acces Manag & S3\imgs\img12.PNG" height="300px" />

<img src="D:\Projectes\Curso_AWS_Architect\Section III Identity Acces Manag & S3\imgs\img13.PNG" height="300px" />

- On **Actions** we canot make it public or it raises and ERROR... We go back to the **S3 Bucket** and select your Bucket and display **Edit public access settings**. 

<img src="D:\Projectes\Curso_AWS_Architect\Section III Identity Acces Manag & S3\imgs\img14.PNG" width="1300px" />

<img src="D:\Projectes\Curso_AWS_Architect\Section III Identity Acces Manag & S3\imgs\img15.PNG" width="300px" />

- Public Access is granted to buckets and objects through **Access Control Lists**, **bucket policies**, **access point policies**... If we Block all public access, it will apply only to the Bucket that is selected and its access points. You click confirm once you choose to **unselect** all options if you want 100% public access.
- Now we can **Make public** the file:

<img src="D:\Projectes\Curso_AWS_Architect\Section III Identity Acces Manag & S3\imgs\img16.PNG" width="400px" />

- **Storage class**:

<img src="D:\Projectes\Curso_AWS_Architect\Section III Identity Acces Manag & S3\imgs\img17.PNG" width="1000px" />



- Such changes can be done in a **Bucket level** or in a **Object Level**
- **Permissions for the Bucket**:
  - Block public access
  - ACL: can go down to objects (you can block one file but let another file be accessible)
  - Bucket policy: make all objects in the bucket PUBLIC (we will do later in the course)
  - CORS configuration
- **Management**:
  - Lifecycle rules (later)
  - Replication (later)
  - Analytics
  - Metrics
  - Inventory

### Summary 3. S3

- All Buckets when created are **PRIVATE** by default. To change them setup access control.

- Buckets are a universal name space
- Upload successful HTTP200 code
- Storage classes
- Control access to buckets using bucket ACL or Bucket Policies (serverless section of course later)



## 4. Security and Encryption

Go to **S3** and click on a Bucket, and click on an Object and go to **Encryption**:

<img src="D:\Projectes\Curso_AWS_Architect\Section III Identity Acces Manag & S3\imgs\img18.PNG" width="300px" />

## 5. Versions

- Store all versions of an object (including all writes and even if you delete an object)
- Great backup tool
- Once enabled on a bucket, it cannot be disabled, **only suspended**. To disable it, you have to **delete a Bucket and create a new one**
- Integrates with **Lifecycle rules** to move thinks to Glacer
- Versioning's **MFA Delete** capability to avoid accidental deletion.



Go to **S3** :

- Create a Bucket

- we **turn Versioning ON**:

  <img src="D:\Projectes\Curso_AWS_Architect\Section III Identity Acces Manag & S3\imgs\img19.PNG" width="300px" />

<img src="D:\Projectes\Curso_AWS_Architect\Section III Identity Acces Manag & S3\imgs\img20.PNG" width="300px" />

- Edit Block Public Access: untick all to make them public
- Upload a file (version 1)
- Enable: Make Public
- Then change locally version 1 file, and upload with the same name
- **When uploading again, the file is NOT PUBLIC!!!** So Make it public again



<img src="D:\Projectes\Curso_AWS_Architect\Section III Identity Acces Manag & S3\imgs\img21.PNG" width="900px" />

- We see that know the size of the bucket is the sum of the two versions (**all versions get stored on the S3 bucket so bear that in mind with big files**). **Maybe you need to enable Lifecycle policy to retire old versions if a lot of versions are accumulated**
- When you upload a new version is private object, but older versions remain public if they were public. 
- **If we delete a file (in the Hide mode in "Versions") that has versioning** we place a **DELETE MARKER**:

<img src="D:\Projectes\Curso_AWS_Architect\Section III Identity Acces Manag & S3\imgs\img22.PNG" width="900px" />

- To **restore** to the latest version we have to **Delete the Delete Marker**:

<img src="D:\Projectes\Curso_AWS_Architect\Section III Identity Acces Manag & S3\imgs\img23.PNG" width="400px" />

- If we **delete the file in "Show" mode in Versions** you delete the version completely.

<img src="D:\Projectes\Curso_AWS_Architect\Section III Identity Acces Manag & S3\imgs\img24.PNG" width="400px" />



## 6. Lifecycle Versioning