# Setting up My GitHub Keys on Windows
One day my GitHub keys suddenly broke for SSH interactions and cloning from my Organizations. This is my personal tutorial on how to fix this. I don't know which steps actually fixed anything.

**Tutorial: Fixing GitHub SSH Issues**

**1. Using Git Bash to Generate PEM Keys:**

Before you start, ensure you have Git Bash installed on your Windows system.

a. Open Git Bash. b. Run the following command to generate a new SSH key using the PEM format:

```bash
ssh-keygen -t rsa -b 4096 -m PEM
```

When prompted to "Enter a file in which to save the key," press Enter to use the default location (`~/.ssh/id_rsa`).

c. You'll then be prompted to enter a passphrase (optional). If you choose to use a passphrase, ensure you remember it or store it securely.

**2. Copying Public Key to Clipboard:**

In Git Bash, run:

```bash
cat ~/.ssh/id_rsa.pub | clip
```

This command copies the contents of your public key file to your clipboard.

**3. Uploading Public Key to GitHub:**

Visit [GitHub SSH Keys](https://github.com/settings/keys) and click on "New SSH key". In the "Key" field, paste your public key from the clipboard. Give it a meaningful title and click "Add SSH key".

**4. Adjusting File Permissions on Windows:**

I then get the following error when running `ssh -vT git@github.com`:

```
debug1: Server accepts key: C:\\Users\\simon/.ssh/id_rsa RSA SHA256:R2xEHr+U2jj7QnlKivyCX0o+95ETUAxwQIAudKrqZ7I
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions for 'C:\\Users\\simon/.ssh/id_rsa' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
Load key "C:\\Users\\simon/.ssh/id_rsa": bad permissions
git@github.com: Permission denied (publickey).
```

To ensure the SSH private key is only accessible by the current user:

- Right-click on the `id_rsa` file located typically in `C:\Users\[YourUsername]\.ssh\`. 
- Choose "Properties" and then go to the "Security" tab.
- Disable inheritance by clicking on "Disable inheritance" at the bottom left
- An option pops up; select "Remove all inherited permissions from this object."
- Apply the changes.
- Add new Permissions only for yourself:

![image](https://github.com/heetbeet/Setting-Up-My-GitHub-Keys-on-Windows/assets/4103775/9862dd0c-149a-4160-8150-7ea7fd465e7e)

![image](https://github.com/heetbeet/Setting-Up-My-GitHub-Keys-on-Windows/assets/4103775/c9d15159-6b7f-43d1-8556-12c9afe14a0f)

![image](https://github.com/heetbeet/Setting-Up-My-GitHub-Keys-on-Windows/assets/4103775/7ff313f7-8034-405d-8df7-9f4e83d103ad)

![image](https://github.com/heetbeet/Setting-Up-My-GitHub-Keys-on-Windows/assets/4103775/ae09965c-1e79-40ff-b964-1c1a3ca883b3)

![image](https://github.com/heetbeet/Setting-Up-My-GitHub-Keys-on-Windows/assets/4103775/17f441c1-a9f5-46d1-916d-c0563de2386e)


**5. Setting Global Git Username and Email:**

a. Set the Git username:

```bash
git config --global user.name "heetbeet"
```

b. Set the Git email to the no-reply GitHub address:

```bash
git config --global user.email "4103775+heetbeet@users.noreply.github.com"
```

To find your own GitHub no-reply email:

* Visit [GitHub Email Settings](https://github.com/settings/emails).
* Look for the section "Keep my email addresses private". Your no-reply email address will be mentioned there.

**6. Activate SSH Agent and Add the SSH Key:**

In Git Bash:

a. Start the SSH agent:

```bash
eval "$(ssh-agent -s)"
```

b. Add your private key to the agent:

```bash
ssh-add ~/.ssh/id_rsa
```

**7. Testing if GitHub Recognizes the SSH Key:**

In Git Bash, type:

```bash
ssh -vT git@github.com
```

If everything is set up correctly, you should receive a message saying, "You've successfully authenticated."
