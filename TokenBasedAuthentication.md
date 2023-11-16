# Creating a GitHub Personal Access Token for Jenkins Authentication

### 1. Log in to GitHub:

Make sure you are logged in to your GitHub account.

### 2. Navigate to Settings:

- Click on your profile picture in the top right corner of the GitHub page.
- Select "Settings" from the dropdown menu.

### 3. Access Developer Settings:

In the left sidebar, click on "Developer settings."

### 4. Generate a Personal Access Token:

- In the Developer settings menu, click on "Personal access tokens."
- Click the "Generate token" button.

### 5. Configure Token Settings:

- Give your token a meaningful name.
- Choose the scopes or permissions based on what your Jenkins job needs to do (e.g., repo, read:user, write:repo_hook).

### 6. Generate Token:

- Scroll down and click the "Generate token" button at the bottom.

### 7. Copy Token:

- Once the token is generated, **copy it immediately.** GitHub will not show it again.

### 8. Store the Token:

- Store the token in a secure place. You might want to use a credential manager or securely store it within Jenkins.



# Configuring a Freestyle Jenkins Job with GitHub Personal Access Token

### 9. Configure Jenkins:

- Open Jenkins and log in to your Jenkins account.
- Navigate to the Jenkins dashboard.
- Click on "New Item" to create a new Jenkins job.
- Enter a name for your job and choose the "Freestyle project" option.
- Click "OK" to create the job.

### 10. Configure Source Code Management:

- In the job configuration page, find the "Source Code Management" section.
- If you are using Git:
  - Select "Git" from the dropdown menu.
  - Enter the Repository URL.
  - In the "Credentials" field, click on the dropdown menu and select "Add" to add a new credential.
  - Choose "Secret text" as the kind of credential.
  - In the "Secret" field, paste the GitHub personal access token that you copied earlier.
  - Optionally, you can provide an ID for the credential and a description.
  - Click "Add" to add the credential.
