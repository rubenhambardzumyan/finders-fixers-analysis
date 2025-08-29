```
Objectstore Project Setup and Compilation Steps
```

- chromeOwner
  - Nitesh Malviya ([nitesh.malviya@trilogy.com](mailto:nitesh.malviya@trilogy.com))
- Purpose
  - To tell each required step to setup the project on EC2 environment.
  - To tell all methods to compile the object store application along with different options
  - To tell about the object store project installation and usage
- DOK2 - Knowledge Base
  - Prerequisite before settings up EC2 machine for DEV and ObjectStore compilation
    - **Kerio Control VPN Client**: Install the KERIO based on [https://docs.google.com/document/d/1GTXN70V5hFv971Ha7_5cVNrEovp6XGg3DzQLdcn3R-E/edit?tab=t.0#heading=h.pkkzcrxmv3jh](https://docs.google.com/document/d/1GTXN70V5hFv971Ha7_5cVNrEovp6XGg3DzQLdcn3R-E/edit?tab=t.0#heading=h.pkkzcrxmv3jh) document.
    - **AWS AD Role**: You must have "RAM-AWS-ObjectstoreDev-Admin" role permission on your AD name. If you haven't raised the access then user [https://supportportal-df.atlassian.net/servicedesk/customer/portal/6/group/76/create/367](https://supportportal-df.atlassian.net/servicedesk/customer/portal/6/group/76/create/367) form with following information
      - Group Name : RAM-AWS-ObjectstoreDev-Admin
      - Active Directory Domain: devfactory.local
      - Active Directory Username: <your AD username>
      - Approving Manager: Thibault Bridel-Bertomeu (thibault.bridelbert) (As your manager for confirmation)
      - Approver AD Username: thibault.bridelbert (As your manager for confirmation)
      - Similarly you need to raise AD role access for following roles
        - VDI2ObjectStoreDevAdminUsers
        - VDI2-Objectstore-Admin
        - VMware-ObjectStore-Dev
        - RAM-PWState-Team-IgniteTech-ObjectStore-Modify
        - RAM-PWState-Product-ObjectStore-Common-Modify
        - VMware-ObjectStore
        - Product-ObjectStore-Engineering
    - **Passwordstate Access**: Passwordstate is a central place for keeping sensitive information like username, passwords and pem or other secret files. If you haven't raised the access then user [https://supportportal-df.atlassian.net/servicedesk/customer/portal/6/group/86/create/490](https://supportportal-df.atlassian.net/servicedesk/customer/portal/6/group/86/create/490) form with following information
      - Product Name : Objectstore
      - Product Access Category : Engineering
  - ObjectStore project setup on AWS EC2 Machine - Launching a new EC2 Instance - You need to be connected the KERIO VPN CLIENT in order to access Passwordstate. - Login to AWS via [https://aws-oidc.devconnect-df.com/credentials/manager](https://aws-oidc.devconnect-df.com/credentials/manager) url using your AD credentials. Click on "Login" in front of "RAM-AWS-ObjectstoreDev-Admin" to login to DEV AWS account of ObjectStore. - Under EC2, Click "Launch Instance". ObjectStore application compilation is dependent upon the Windows server version along with VS Code. AWS has AMI's for different versions so choose your AMI based on the requirement. This EC2 Machine will not have the public IP and will be access via private ip. You have to be connected to KERIO VPN CLIENT to access EC2 machine - Under "Application and OS Images", choose "My AMI" and choose the AMI - 2016 : ami-028224487f987c6d0 - 2019 : ami-03fe7e8eef64a6dd6 - 2022 : ami-0b77807b0ba71f551 - Choose "Instance Type", You will need atleast 2 core 8GB machine for compilation of object store. - VPC: vpc-08d0e87a685285f7b - Subnet: subnet-0bff8e6248fe6ab18 - Auto Assign Public IP: Disable - Security Group: sg-0a54d29e43c4ed68f - Advance details -> IAM Instance Profile -> AmazonSSMRoleForInstancesQuickSetup - Click "Launch Instance" to launch a new EC2 machine. Ensure that you are connected to "KERIO VPN CLIENT" otherwise you will not be able to connect to EC2 via "Private IP" - Use "Windows Remote Desktop" to connect to EC2 machine via "Private IP" with userid and password mentioned under passwordstate. The userID and password are dependent upon the AMI which you used to create the instance - 2016 : [Windows nt2016-pbld](https://workflowy.com/s/objectstore-project/NhAaDAbk0M5lj2DB) - 2019 : [Windows nt2019-pbld](https://workflowy.com/s/objectstore-project/NhAaDAbk0M5lj2DB) - 2022 : [Windows nt2022-pbld](https://workflowy.com/s/objectstore-project/NhAaDAbk0M5lj2DB) - This EC2 Machine has all prerequisite installed which are required for compiling the "ObjectStore" application. - Check if EC2 machine is properly connected to domain controller or not. - Once the EC2 machine is running and you are logged to machine via local administrator credentials (from "passwordstate") and open the powershell (Run as Administrator - Run the following command and check if this returns "true" or "false". If the following command returns "true" then your machine is connected to domain controller "objectstore.local". You can skip this section. - ```
    Test-ComputerSecureChannel -Verbose

````
      - If the above command fails and give the output "false" then your machine is not connected to domain controller "objectstore.local" and has broken trust.
      - Connect EC2 Machine to Domain Controller if trust is broken
        - Method 1 :
          - Open powershell as administrator.
          - Run the following command to repair the trust. Enter the domain administrator userid and password (PasswordState->ObjectStore->Common->OStoreDC01). Restart the Machine.
          - ```
Test-ComputerSecureChannel -Repair -Credential (Get-Credential)
````

          - Again run the following command and see if the output is true or not. If its still false then follow the method 2
          - ```

Test-ComputerSecureChannel -Verbose

````
        - Method 2 : Only if Method 1 fails
          - Right click "This PC" and click "Properties" and under "Computer Name, Domain and Workgroup Settings" section click on "Change Settings"
          - If the "System Properties" windows shows "objectstore.local" then first you need to remove the machine from domain.
          - Click "Change" and from "Computer Name/ Domain change" popup select "Workgroup" and enter "WORKGROUP" and click OK. Enter the domain administrator userid and password (PasswordState->ObjectStore->Common->OStoreDC01). Restart the Machine.
          - Login to DOMAIN CONTROLLER machine from windows remote desktop. (PasswordState->ObjectStore->Common->OStoreDC01).
            > NOTE: YOU DO NOT NEED TO RESTART THIS SYSTEM AFTER THE FOLLOWING CHANGES. BE CAREFUL WITH THIS SYSTEM
            >
            - Click Start and type "DNS" and open "DNS Manager"
              - Go to OSTOREDC1-> Forward Lookup Zone -> objectstore.local
              - Check if your VM is there in the list of not. If not right click "objectstore.local" from left menu and select "New Host (A or AAAA)"
              - Enter unique machine name "NT2019-XYZ" and enter the private IP of your EC2 and click OK. Refresh to see the newly added host.
            - Click Start and type "dsa.msc" and open "Active Directory Users and Computers"
              - Navigate to "objectstore.local"->computers and see if you computer name appears here. If yes then remove and if no then no action required.
          - Once your EC2 machine restarted after the workgroup change (your EC2 machine not domain controller) perform the following changes in order to setup the trust again to domain "objectstore.local"
            - Right click "This PC" and click "Properties" and under "Computer Name, Domain and Workgroup Settings" section click on "Change Settings".
            - Enter the "Computer Name" same as which you kept in "Domain Controller" while adding as host to "Forward Lookup Zone" i.e. NT2019-XYZ. System will ask for restart so please restart.
            - Then again right click "This PC" and click "Properties" and under "Computer Name, Domain and Workgroup Settings" section click on "Change Settings".
            - Select domain and enter "objectstore.local". It will prompt for the authentication. Enter the domain administrator userid and password (PasswordState->ObjectStore->Common->OStoreDC01). If successful you will see "Welcome to objectstore.local". Restart the Machine.
            - Now run the following command and it should return true
            - ```
Test-ComputerSecureChannel -Verbose
````

    - Setting up project in EC2 instance
      - Create a work folder in C: drive and clone the project
      - ```

cd C:\
mkdir work
cd work
git clone https://github.com/apache/ignite-objectstore.git src

````
      - Open the "src" folder into "Visual Studio 2022" and let the makefile process complete.
    - KERBEROS Domain query and setup guide
      - Domain Membership (Run on client, server and domain controller machine)
        - Ensure all machines (client, remote server, and domain controller) are joined to the same Active Directory domain.
        - ```
systeminfo | findstr /C:"Domain"

````

        - Expected output: "objectstore.local"
      - Service Account and Identity (Run on both client and server machine)
        - Determine which account the service (ObjectStore) is running under.
        - ```

sc.exe qc "ObjectStore Server R2024"

````
        - Expected output: "SERVICE_START_NAME : LocalSystem"
      - Time Synchronization  (Run on client, server and domain controller)
        - Kerberos allows only 5 minutes of clock skew. Ensure all machines are time-synced.
        - ```
w32tm /query /status

````

        - Expected output: Client and server should show source as "objectstore.local" and domain controller should show source as "ntp"
        - If the sources are not correct on client and server then
          - ```

w32tm /config /syncfromflags:domhier /update
net stop w32time
net start w32time
w32tm /resync

````
        - If the source is not correct on the domain controller
          - ```
w32tm /config /manualpeerlist:"time.windows.com,0x9" /syncfromflags:manual /reliable:YES /update
net stop w32time
net start w32time
w32tm /resync

````

      - DNS Configuration (Run on client machine)
        - Use fully-qualified domain names (FQDNs) in SPNs and client connections. Do not use IPs or aliases.
          - ```

nslookup nitesh-slave.objectstore.local

````
        - Expected output: It should print the IP of the server machine
      - Domain Controller Connectivity (Run on both client and server machine)
        - Verify client and server can discover the domain controller and its KDC role.
          - ```
nltest /dsgetdc:objectstore.local /force /kdc

````

        - Expected output: Domain controller name and IP and flags including kdc
      - SPN Configuration (Run on Domain controller)
        - SPN can be registered for both "Machine Account" as well as "Domain Account".
        - Kerberos can work for both "Machine account" or "Domain Account" with registered SPN.
          - Machine Account: Verify that the required Service Principal Name (SPN) is registered.
            - ```

To check the SPN registered under Machine account

setspn -L <remote server machine name i.e. nt-test-slave>

````
            - ```
If you want to register a new SPN under machine account then first check if the SPN already exist to avoid duplicate SPN

setspn -Q <new desired SPN>
````

            - ```

If the SPN does not exist then create new SPN

setspn -S <new desired SPN> <remove server machine name i.e. nt-test-slave>

````
          - Domain User: Verify that the required Service Principal Name (SPN) is registered.
            - ```
To check the SPN registered under Domain account

setspn -L <domain user account i.e. objectstore.local\Administrator>
````

            - ```

If you want to register a new SPN under machine account then first check if the SPN already exist to avoid duplicate SPN

setspn -Q <new desired SPN>

````
            - ```
If the SPN does not exist then create new SPN

setspn -S <new desired SPN> <domain user account i.e. objectstore.local\Administrator>
````

      - List cached KERBEROS ticket
        - Run the command "klist" to see all cached KERBEROS tickets
        - Run the command "klist purge" to remove all existing ticket.

- ObjectStore application compilation - ObjectStore compilation generate three type of builds i.e. debug, symbol and retail. "debug" as name suggest is used for debugging purpose and "retail" is used for release. - After the compilation, packing will generate the executables "exe" of the application which can be used to installed objectstore application. - Build logs will be available at "C:\work\logs". You can search for the specific "debug" or "retail" target logs in this folder. - Builds will be available in "C:\work\build" folder. - Open "X64 native tools command prompt" in administrator mode. - There are three ways to compile the objectstore application - Method 1 (via builder.bat command) - This is the most easy way to compile the application but it will generate all three type of builds i.e. debug, symbol and retail so it will take time in compilation process. - It can be used to both compile and package the application via single command. - In "X64 native tools command prompt", navigate to "C:\work\src" - Then run the "builder.bat" command. It will ask some questions as following - UPDATE_BUILD_CONFIG=Update build configuration? (Y/N) : If you want to change the current build configuration then you should say Y otherwise N. Current configuration can be seen just above this message in command prompt in the following format - ```
  C:\work\src>echo Current build configuration:
  Current build configuration:

C:\work\src>echo Architecture: amd64
Architecture: amd64

C:\work\src>echo Visual Studio: vs2022
Visual Studio: vs2022

C:\work\src>echo Build steps: bld pkg
Build steps: bld pkg

C:\work\src>echo Continue on error: 0 (0=No, 1=Yes)
Continue on error: 0 (0=No, 1=Yes)

````
          - Select architecture: Current objectstore is only supporting "AMD64" so you should choose 2 from following
          - ```
C:\work\src>echo Available architectures:
Available architectures:

C:\work\src>echo 1. x86
1. x86

C:\work\src>echo 2. amd64
2. amd64

C:\work\src>set /p "ARCH_CHOICE=Select architecture (1-2): "
Select architecture (1-2):
````

          - Select Visual Studio Version: Select the version based on the visual studio which you are running
          - ```

C:\work\src>echo Available Visual Studio versions:
Available Visual Studio versions:

C:\work\src>echo 1. VS 2022

1. VS 2022

C:\work\src>echo 2. VS 2019 2. VS 2019

C:\work\src>echo 3. VS 2017 3. VS 2017

C:\work\src>echo 4. VS 2015 4. VS 2015

C:\work\src>echo 5. VS 2013 5. VS 2013

C:\work\src>echo 6. VS 2012 6. VS 2012

C:\work\src>echo 7. VS 2010 7. VS 2010

C:\work\src>set /p "VS_CHOICE=Select Visual Studio version (1-7): "
Select Visual Studio version (1-7):

````
          - Include package step: Select "Yes" if you want to package the application after the build process otherwise it will only build and will not package.
          - ```
C:\work\src>set /p "INCLUDE_PKG=Include package step? (Y/N): "
Include package step? (Y/N):
````

          - Include TSD tests: Select "Yes" if you want to include
          - ```

C:\work\src>set /p "INCLUDE_TSD=Include TSD tests? (Y/N): "
Include TSD tests? (Y/N):

````
          - Include unit tests: Select "yes" if you want to execute unit test after the successful build
          - ```
C:\work\src>set /p "INCLUDE_UNIT=Include unit tests? (Y/N): "
Include unit tests? (Y/N):
````

          - Continue on build step failure: Select 1 if you want to continue even some steps in build failed. Mostly select "0=No" to not continue on intermediate step failure.
          - ```

C:\work\src>set /p "CONTINUE_ON_ERROR=Continue on build step failure? (0=No, 1=Yes): "
Continue on build step failure? (0=No, 1=Yes):

````
      - Method 2 (via nt_setup.cmd command)
        - This is similar version to builder.bat but it has more granular control. You can generate only debug output from this method.
        - In "X64 native tools command prompt", navigate to "C:\work\src\tests\osci" and then the command ".\nt_setup.cmd". Answer the question as following
          - Select the platform you are building on(default x86): x86(32-bit) or x64(64-bit).
            - [x86]:  x64
          - Enter the full directory path where the src directory resides, for example, C:\R7.4:  C:\work
          - Do you want to build an ObjectStore debug tree (Y/N) [Y]:  Y
          - Do you want to build an ObjectStore retail tree (Y/N) [N]:  N
          - Do you want to build an ObjectStore debugopt tree (Y/N) [N]:  N
          - Do you want to build an ObjectStore symbol tree (Y/N) [N]:  N
          - Do you want Visual C++ browser support (Y/N) [Y]:  Y
          - Do you want to run the unit tests (Y/N) [Y]:  Y
          - Do you want to setup the test suite (Y/N) [Y]:  N
      - Method 3 (via winnt.bat command)
        - This is the most configurable method and it does not have any prebuild questions to answer
        - In "X64 native tools command prompt", navigate to "C:\work\src\osci\scripts\build_test\nt\batch_conf_TeamCity".
        - Run the following commands to set the environment variables. Please note that these environment variables are set for this command prompt session only. If you open another command prompt then you have to set the following environment variables separately for that session too.
        - ```
set REMOTE_MACHINE=nt-test-slave
set LOCAL_MACHINE=%COMPUTERNAME%
set OS_USERNAME=test1
set OS_PASSWORD=G0ForIt
set OS_USE_INET6=0
set JENKINS_URL="asdasdasdasd"
set NODE_NAME=ObjectStore-win2-5
````

        - To build the project for "debug" you can run the following command. If you want to build for "retail" then you can change "debug" to "retail". If you will not pass anything then it will build all three i.e. debug, symbol and retail builds.
        - ```

winnt.bat amd64 vs2022 bld debug

````
        - To package the project you can run the following command. The packaged executable will be available at "c:\work\package" folder
        - ```
winnt.bat amd64 vs2022 pkg
````

- ObjectStore application installation
  - After the compilation and packaging, it will generate a package folder at "C:\work\package" folder.
  - Inside "C:\work\package\ostore" you will find a "setup.exe" which is a package installer for objectstore.
  - Installation of the objectstore will involve following
    - **Enter your information. Enter your name and organisation. This has no impact.**
    - **Select the licence. You can select the licence from "C:\work\src\tests\osji\java\unit\com\odi\test\license" location. **
    - **Do you want to change the server parameter? If you want to install the application to test against some other server then you can provide that server name otherwise this application will connect default to "nt-test-slave" server.**
    - **Do you want to create RAWFS partition. You can create this partition or skip it.**
    - **Do you want to create the server logs?**
  - Once "ObjectStore" application is installed then you can see it running under services. To view, in the start menu search for "services" and open the services. Scroll down and you will see following two services running
    - **Cache**
    - **Server**
- ObjectStore Environment variables
  - ObjectStore application use different environment variables to alter the settings. Following is the list of some important environment variables along with the way to create/update
    - In the start menu, search for "regedit". It will open the "REGISTERY EDITOR". In the left menu click on "HKEY_LOCAL_MACHINE-> System -> Current Control Set -> Services -> ObjectStore Server/ ObjectStore Cache Manager". You will see three entries under "OBJECT STORE"
      - **Server**
      - **Server**
      - **Server**
    - You can also add environment variable via "System Variables". In the start menu, search for "system environment" and it will show "Edit System Environment Variables".
      - Open the "Advanced" tab and click on "Environment Variable"
      - Under "System Variable" section you can set the desired environment variables.
    - Once you edit the environment variable then you need to restart the "ObjectStore" service in order to take them into effect.
      - To restart the "ObjectStore" service, search for "services" in the start menu and open the services. Scroll down and restart both "Objectstore cache" and "Objectstore server" services.
- ObjectStore application debugging
  - "ObjectStore" application has difference debug levels for both "ObjectStore cache" and "Objectstore server" services.
    - Click WIN+R and type "regedit". It will open the registry editor.
    - Go to "HKEY_LOCAL_MACHINE-> System -> Current Control Set -> Services -> ObjectStore Server/ ObjectStore Cache Manager"
    - Search for key with name "ImagePath"
    - Stop the service by WIN+R and type "services" and search for "ObjectStore Server" and hit stop.
    - What ever value it has, put "-d 9" at the end.
    - Start the service again.
    - Now you should be able to see the logs at "<ObjectStore Installation Directory>\temp\osserver.txt"
  - Check the audit for success/ failure of login/ logoff events
    - Press Win + R then type: "eventvwr.msc" and then enter.
    - Navigate to "Event Viewer > Windows Logs > Security" to view the audit events.
- DOK1 - Facts
  - Developers has two ways to do the development on "objectstore" project
    - Settings up their own machine (Windows or Linux):
      - The local windows of linux setup is fully documented [https://github.com/trilogy-group/ignite-objectstore](https://github.com/trilogy-group/ignite-objectstore). You can following the windows or linux installation guide and complete the setup step by step.
      - Since its required lot of changes and software installation so its recommended to use separate virtual machine for this setup
    - Setting up EC2 machine on AWS
      - This is easy as compared to setting up your own machine because this has ready to go AMI available on AWS to spun up new instance to start the development.
      - You need to ensure that your machine is in the domain "objectstore.local" and has secure connection established between your and domain controller machine.
-
