
# To manage two different GitHub accounts on Ubuntu 22.04 using SSH keys, follow these steps:

## 1. Generate SSH Keys for Each Account

1.1) Open a terminal and run:

ssh-keygen -t ed25519 -C "personal@email.com" -f ~/.ssh/id_github_personal

Example: 

ssh-keygen -t ed25519 -C "arundhwajiiith@gmail.com" -f ~/.ssh/id_github_arun

1.2) Press Enter to leave the passphrase empty (or set one if preferred).

....

It will create two files:

~/.ssh/id_github_arun

~/.ssh/id_github_arun.pub

## 1.3) Edit/Create ~/.ssh/config 

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


## 1.4) Change the Permissions: Ensure SSH files have correct permissions

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


## 4) Clone Repositories Using SSH Aliases

4.1) Use the custom host aliases when cloning:

#### //documentation repo in personal account: 

git clone git@arun:personal_username/documentation.git

Example: 

$ git clone git@arun:ArunDhwajIIITH/repo.git


## 5) Update Existing Repository Remotes

5.1) If you have existing repos, update their remote URLs:


cd /path/to/personal-repo

git remote set-url origin git@personal.github.com:personal_username/repo.git


cd /path/to/work-repo

git remote set-url origin git@work.github.com:work_username/repo.git


## 6) Optional: Configure Local Git User Info

6.1) Set the user.name and user.email per repository to match commits:

#### For personal repos

a) git config user.name "Personal Name"

Example: 

$ git config user.name "Arun Dhwaj"

b) git config user.email "personal@email.com"

Example:

$ git config user.email "arundhwajiiith@email.com"


## 7) Set global username and email

git config --list  # Shows all settings (global + local)

git config --global user.name "ArunDhwajIIITH" # Checks only global

git config --local --get user.name   # Checks only the current repo

