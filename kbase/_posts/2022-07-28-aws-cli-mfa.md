---
layout: post
title: AWS CLI - Connect with MFA
description: >
  Connecting to the AWS CLI when MFA is enforced for your AWS user account.
categories: [kbase]
tags:       [aws, multi-os, sysops]
---
# AWS CLI - Connect with MFA

## Purpose
To follow good security practices, it is recommended to enforce Multi-Factor Authentication (MFA) for all IAM user accounts within an AWS account. To execute commands via the AWS CLI/SDK’s when MFA has been enforced, it is then required to authenticate with MFA before those commands can be executed successfully. The following post outlines a process to facilitate easier authentication using MFA via the CLI/SDK interfaces than the official AWS solution.

## Assumptions
A number of assumptions have been made when compiling the below procedure. They include:
+ The user for which MFA access is being enabled has access (both programmatic and console) to an AWS account.
+ MFA has already been setup on the user's AWS IAM account.
+ Familiarity with the terminal environment for the operating system being used.
+ Python 3 (and pip) are setup and working and have been added to the `$PATH` variable.
+ Familiarity with AWS CLI profiles.
+ A profile for the desired IAM user account has already been setup on the computer.

## Background
The official AWS guide to setup MFA via the terminal can be found at the following link:  
<https://aws.amazon.com/premiumsupport/knowledge-center/authenticate-mfa-cli/>{:target="_blank"}

While the official guide can be used to connect to the AWS CLI, it is cumbersome and requires manual editing of config files whenever the MFA token expires. Using a third party package allows for a much more streamlined experience for the user. The package utilised in this guide is linked below:  
<https://github.com/broamski/aws-mfa>{:target="_blank"}  
The package repository lists in depth usage instructions that were used to create this guide.

## Procedure
To install and use the aws-mfa package:
1. Open a terminal application and execute:  
```shell
pip install aws-mfa
```

2. The default aws-mfa setup uses an AWS profile suffix of `-long-term` to denote the profile without MFA and no suffix for an MFA enabled profile. To make it easier to enter the long term profile, this guide will use the suffix `-lt` for long term credentials.
To setup a new MFA enabled profile, execute the following command, ensuring to update the arguments with the user's details:
```shell
aws-mfa --duration 43200 --device arn:aws:iam::123456789112:mfa/username --profile my-profile --long-term-suffix lt
```
<u>Arguments</u>
>\-\-duration 43200
>: Set code to expire after 12 hours (43200 seconds).
>
>\-\-device
>: The arn for the user's MFA device in AWS. Can be found in the AWS console on the Security Credentials page.
>
>\-\-profile
>: An existing AWS long term profile to enable MFA on.
>
>\-\-long-term-suffix
>: The suffix to add to the existing long term profile.

3. After executing step 2, a prompt to enter a code from the MFA device will be displayed. Enter the code followed by the return key to setup MFA.

4. The MFA profile can now be used by entering the original AWS long term profile name along with AWS CLI commands using the `--profile` argument as would have been the case before setup. To execute a command without MFA, add the `-lt` suffix to the original profile name (e.g. `default-lt`).


5. *(Optional)* To facilitate faster authentication, an alias can be used within the terminal environment. This step can be repeated for any number of AWS profiles as required.  
The process differs slightly dependant on OS:
   1. **Debian based Linux Bash Shell**  
   Append to or create a file named `.bash_aliases` in the user's home directory and enter the command from step 2 on a new line using the `alias` command then restart the terminal environment.  
   Be sure to change `my-alias-name` to the required alias and update the command arguments per step 2:
   ```shell
   alias my-alias-name="aws-mfa --duration 43200 --device arn:aws:iam::123456789112:mfa/username --profile my-profile --long-term-suffix lt"
   ```
   2. **Mac OSX Bash or Zsh Shell**  
   Append to or create a file named `.bash_profile` (for Bash) or `.zshrc` (for Zsh) in the user's home directory and enter the command from step 2 on a new line using the `alias` command then restart the terminal environment.  
   Be sure to change `my-alias-name` to the required alias and update the command arguments per step 2:
   ```shell
   alias my-alias-name="aws-mfa --duration 43200 --device arn:aws:iam::123456789112:mfa/username --profile my-profile --long-term-suffix lt"
   ```
   3. **Windows Powershell**  
   Append to or create a file named profile.ps1 the user's $Home\Documents directory and enter the command from step 2 on a new line using the `Set-Alias` cmdlet then restart the terminal environment.  
   Be sure to change `my-alias-name` to the required alias and update the command arguments per step 2:
   ```powershell
   Function my-alias-name {aws-mfa --duration 43200 --device arn:aws:iam::123456789112:mfa/username --profile my-profile --long-term-suffix lt}
   Set-Alias -Name my-alias-name -Value my-alias-name
   ```

## Conclusion
After following the above procedure, authentication to AWS should be possible using MFA from the CLI through the use of the aws-mfa package.

To renew an expired token, the command in step 2 can be rerun and a new MFA code entered.
If using the optional alias command, entering the selected `my-alias-name` alias will prompt for the code without requiring additional arguments.

Running the preferred command on an unexpired token will result in the time to expiry (in seconds and UTC) being returned.