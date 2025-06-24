Using --global flag to set name/email for global commits (personal one recomended)
```bash
git config --global user.name "Your Name"
git config --global user.email "Your Email"
```

Check it
```bash
git config --global --list
```

For work can be set locally in the project folder by navigating with ```shell cd``` to it and setting (No need if using WebStorm, menage it by itself):
```bash
git config user.name "Work Name"
git config user.email "Work Email"
```

Adding SSH-key 
```bash
ssh-keygen -t ed25519 -C "email"
```

After entering command above it will ask to enter name of the file in witch key will be saved

Adding SSH-key to the SSH agent
```bash
ssh-add name_of_SSH_key
```

To copy SSH key and add it to the GitHub Account
```bash
cat name_of_SSH_key.pub
```

Going into GitHub -> Settings -> New SSH key
![[Pasted image 20250624102205.png]]![[Pasted image 20250624102300.png]]

For setting personal and work accounts separately must add config file in the .ssh hidden folder in the root, there we can move all created before SSH-key files and add new text file with next content:
```text
# Personal GitHub
Host github-personal
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ssh_personal
  IdentitiesOnly yes

# Work GitHub
Host github-work
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ssh_work
  IdentitiesOnly yes
```

To check does it work type
```bash
ssh -T git@github-personal #For personal
ssh -T git@github-work #For work
```
Expected result ```Hi, Name of your personal or work GitHub account```

Practical use: when coping repo from GitHub we can use 
```bash
git clone git@github-personal:your-username/repo.git
```

Mostly will use for personal not web project probably as WebStorm handles most of git operation by UI.

Adding Personal Access token
```
GitHub -> Setting -> Developer Setting(at the very buttom) ->  Personal access tokens ->  Generate new token -> Generate new token(classic)
```
Type name of the token, expiration date (recommended not to use 'No expiration' as it is not safe), select scopes
Copy token and save it somewhere save, use where needed(WebStorm)


