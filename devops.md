
# To manage two different GitHub accounts on Ubuntu 22.04 using SSH keys, follow these steps:

## 1. Generate SSH Keys for Each Account

### 1.1) Open a terminal and run:

ssh-keygen -t ed25519 -C "personal@email.com" -f ~/.ssh/id_github_personal

Example: 

ssh-keygen -t ed25519 -C "arundhwajiiith@gmail.com" -f ~/.ssh/id_github_arun

### 1.2) Press Enter to leave the passphrase empty (or set one if preferred).

....

It will create two files:

~/.ssh/id_github_arun

~/.ssh/id_github_arun.pub

### 1.3) Edit/Create ~/.ssh/config 

nano ~/.ssh/config

#### //Personal GitHub Account

Host arun

    HostName github.com

    User git

    IdentityFile ~/.ssh/id_github_arun

    IdentitiesOnly yes


#### //Work GitHub Account

Host work

    HostName github.com

    User git

    IdentityFile ~/.ssh/id_github_work

    IdentitiesOnly yes


### 1.4) Change the Permissions: Ensure SSH files have correct permissions

a) chmod 600 ~/.ssh/id_github_*

b) chmod 644 ~/.ssh/config

c) $ chmod 600 ~/.ssh


## 2) Updating the data on github: Add SSH Keys to GitHub Accounts

2.1) Display the public keys and copy them:

cat ~/.ssh/id_github_arun.pub

2.2) Login to GitHub: 

(profile picure/icon) - -> Settings --> SSH and GPG Keys for each account and add the respective keys.

2.3) Click on "New SSH Key"(Location: top right corner)

2.4) Add the followings:
a) Title: Enter suitable title,
b) Key type: select "Authentication key"
c) key: paste ( the data copied from 'cat ~/.ssh/id_github_arun.pub' )


## 3) Test the SSH Connections

3.1) Verify authentication for personal account: <arun>:

$ ssh -T git@arun

>> Hi <username>! You've successfully authenticated...


## 4.1) Set global username and email ==> It has global effect. Means into all the repositories on the local machine.

a) git config --list  # Shows all settings (global + local)

>> Display the global config

b) git config --global user.name "ArunDhwajIIITH" # Checks only global

c) git config --global --get user.email  "arundhwajiiith@gmail.com" 


## 5) Clone Repositories Using SSH Aliases

### 5.1) Very important: Use the custom host aliases when cloning:

a) Login to github account,

b) select the Organisation,

c) select the repository -- > Go on <code> --> Local --> clone --> ssh --> click on copy

>> git@github.com:sbpenterprise5thattempt/sbp-vc-frontend-new.git

d) Very important change it to 

$ git clone git@arun:sbpenterprise5thattempt/sbp-vc-frontend-new.git


e) Do the needful change in repo. Add, commit, push

