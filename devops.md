
# To manage two different GitHub accounts on Ubuntu 22.04 using SSH keys, follow these steps:

## 1. Generate SSH Keys for Each Account

1.1) Open a terminal and run:

ssh-keygen -t ed25519 -C "personal@email.com" -f ~/.ssh/id_github_personal
ssh-keygen -t ed25519 -C "work@email.com" -f ~/.ssh/id_github_work

1.2) Press Enter to leave the passphrase empty (or set one if preferred).


## 2. Add SSH Keys to GitHub Accounts

2.1) Display the public keys and copy them:

cat ~/.ssh/id_github_personal.pub
cat ~/.ssh/id_github_work.pub


2.2) Go to GitHub → Settings → SSH and GPG Keys for each account and add the respective keys.


## 3. Configure SSH to Handle Multiple Keys

3.1) Create/edit the SSH config file:

nano ~/.ssh/config


3.2) Add the following entries (replace personal.github.com and work.github.com with aliases of your choice):

### //Personal GitHub Account
Host personal.github.com
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_github_personal
    IdentitiesOnly yes

### //Work GitHub Account
Host work.github.com
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_github_work
    IdentitiesOnly yes


## 4. Test the SSH Connections

4.1) Verify authentication for both accounts:

ssh -T git@personal.github.com
ssh -T git@work.github.com


4.2) You should see success messages like:

Hi <username>! You've successfully authenticated...


## 5. Clone Repositories Using SSH Aliases

5.1) Use the custom host aliases when cloning:

### //Personal repo
git clone git@personal.github.com:personal_username/repo.git

#### //Work repo
git clone git@work.github.com:work_username/repo.git


## 6. Update Existing Repository Remotes

6.1) If you have existing repos, update their remote URLs:


cd /path/to/personal-repo
git remote set-url origin git@personal.github.com:personal_username/repo.git


cd /path/to/work-repo
git remote set-url origin git@work.github.com:work_username/repo.git


## 7. Optional: Configure Local Git User Info

7.1) Set the user.name and user.email per repository to match commits:

# For personal repos
git config user.name "Personal Name"
git config user.email "personal@email.com"

# For work repos
git config user.name "Work Name"
git config user.email "work@email.com"


## 8. Permissions: Ensure SSH files have correct permissions

chmod 600 ~/.ssh/id_github_*
chmod 644 ~/.ssh/config







