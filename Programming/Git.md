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
