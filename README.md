# DSC-unencryptedCredsDemo
A use case - and warning about - Powershell Desired State Configuration plaintext passwords

Files contained in this archive:

*unencryptedCredentials.ps1* : A PowerShell script file containing a Configuration function and Configuration Data.
This configuration is intended as a use case for DSC Plaintext passwords (`PSDscAllowPlainTextPassword`). A variety of methods for storing and retrieving the password are used. All of these are **extremely unsecure**.

*"\unencryptedPasswordDemo"* : Contains the MOF files generated as a result of running the aforementioned configuration. **These MOFs contain passwords in plain text**. This is included to demonstrate how easy it is to recover passwords when you use the insecure option. These MOF files are also present on the managed node, which means anyone with access to either computer now has access to the local administrator password.
Specifically,
```
instance of MSFT_UserResource as $MSFT_UserResource1ref
{
Password = "ThisIsAPlaintextPassword";
 UserName = "badIdea";

};

instance of MSFT_Credential as $MSFT_Credential2ref
{
Password = "a password, in plaintext";
 UserName = "zach";

};

instance of MSFT_Credential as $MSFT_Credential1ref
{
Password = "ThisIsYetAnotherPlaintextPassword";
 UserName = "zach";

};
```


For information on how to **securely** store passwords using Desired State Configuration, refer to this TechNet documentation https://technet.microsoft.com/en-us/%5Clibrary/Dn781430.aspx

