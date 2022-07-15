<!-- markdownlint-configure-file {
  "MD013": {
    "code_blocks": false,
    "tables": false
  },
  "MD033": false,
  "MD041": false
} -->

<div align="center">

# Redinger Transition of Power

Everything to know for my transition out of Denver Health Help Desk

</div>

## Table of Contents

- [Access](#access)
  - [AWS](#whale-access-aws)
  - [Trello](#books-access-trello)
  - [Scripts](#clipboard-scripts)
- [Trello](#books-trello)
- [Webex Bot](#pizza-webex-bot)
  - [Starting](#star-starting)
  - [Updating](#hammer-updating)

## :lock: Access

All pertinent access changes will be listed below - proceed to the individual section in order to learn more.

- Transfer ownership of `AWS` EC2 T2.micro instance
- Transfer ownership of `Trello` General Project List ([assisted process](https://support.atlassian.com/trello/docs/how-to-transfer-boards-to-a-new-account/))
- Transfer `Powershell` and `Python` scripts from personal H drive (manual process)

### :whale: Access (AWS)

In order to transfer an EC2 instance, you will be using a [manual process](https://aws.amazon.com/premiumsupport/knowledge-center/account-transfer-ec2-instance/).

<details><summary><b>Transfer EC2 Instance</b></summary><br>

1. Create a custom AMI
2. Share the AMI with the target account
3. From target account, find the shared AMI
4. Launch a new instance from the shared AMI
    - May need to import a key pair
5. Create a custom AMI from the target account instance
6. Deregister the AMI on the source account

</details>

<details><summary><b>AWS Account Provisioning/IAM</b></summary><br>

Provision user IAM policies [here](https://console.aws.amazon.com/iam/home).

Do **NOT** use the root user as your main user.

Create a new user with at least the following permission policies attached to the account:
- AmazonEC2FullAccess

</details>

### :books: Access (Trello)

In order to transfer a Trello board, you can use Trello's assisted board transfer support page located [here](https://trello.com/support/transfer-boards).

<details><summary><b>Transfer Trello Board</b></summary><br>

1. Log into source account
2. Go to https://trello.com/support/transfer-boards and enter target account username or email address
3. Select boards to transfer
4. Remove source account from boards
5. Transfer boards

</details>

### :clipboard: Scripts

All Denver Health-related project source files (including random nonsense :smile:) are located in H:\Projects - specifics are listed below:

- `Tier 3 Inventory`
  - [QR Codes](H:\Projects\Excel\Inventory)
- [`Powershell Scripts`](H:\Projects\PowerShell), notably:
  - FindUser.bat/.ps1
  - GetComputerInfo.bat/.ps1
  - CompareGroups.bat/.ps1
- [`Python Scripts`](H:\Projects\Python), notably:
  - [Webex Bot](H:\Projects\Python\DHHD-Webex-Bot)
- [`Random Batch Scripts`](H:\Projects\Batch), notably:
  - XenMobileGroups.bat
  - RemoteControl.bat
  - mg.cmd
- [`Cherwell KAs`](H:\Projects\Cherwell)

---

## :books: Trello



- [General Project List](https://trello.com/b/BTQeLHSP/general-project-list)

## :pizza: Webex Bot

The bot lives on an AWS EC2 server located in US West (N. California) region. In order to stop/start/update the bot, you must log directly into the instance via the EC2 management console [here](https://us-west-1.console.aws.amazon.com/ec2/v2/home?region=us-west-1#Instances:v=3). Provided the user account has been provisioned correctly, you can connect via the EC2 Instance Connect option (leave the username as is).

### :star: Starting

> 💡 Make sure to be connected to the EC2 instance before running these scripts.

<details><summary><b>How to start the bot</b></summary><br>

1. Change directory into working directory:

  ```bash
  $ cd /home/ubuntu/dhwebexbot
  ```

2. Run program without hangup (will not stop on console exit):

  ```bash
  $ nohup python3 ./main.py &
  ```

3. Verify script is running:

  ```bash
  $ ps ax | grep main.py
  ```

</details>

### :hammer: Updating

> 💡 Any updates to the script will need to be [committed to GitHub](https://github.com/git-guides/git-commit) prior to the following script.<br>
> 💡 You will need to [set up a personal access token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token) via GitHub prior to cloning the repository.

<details><summary><b>How to pull updates</b></summary><br>

1. Change directory into working directory:

  ```bash
  $ cd /home/ubuntu
  ```

2. Get running processes where script is running:

  ```bash
  $ ps ax | grep main.py
  ```

3. Kill running process:

  ```bash
  $ kill {PSID}
  ```

4. Remove deprecated folder:

  ```bash
  $ rm -rf dhwebexbot
  ```

5. Clone repository from GitHub to `dhwebexbot` folder:

  ```
  $ git clone https://{username}@github.com/{username}/dhhd-webex-bot dhwebexbot
  ```

</details>
