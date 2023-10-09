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

To ensure the SSH private key is only accessible by the current user:

a. Right-click on the `id_rsa` file located typically in `C:\Users\[YourUsername]\.ssh\`. b. Choose "Properties" and then go to the "Security" tab. c. Click on the "Advanced" button. d. At the top of the window that opens, there's an "Owner" field. Ensure you are the owner. If not, click "Change" and set yourself as the owner. e. Disable inheritance by clicking on "Disable inheritance" at the bottom left. f. An option pops up; select "Remove all inherited permissions from this object." g. Apply the changes and ensure only your user account has access.

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
ssh -T git@github.com
```

If everything is set up correctly, you should receive a message saying, "You've successfully authenticated."
