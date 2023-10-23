![Build Status](https://camo.githubusercontent.com/6e661d9391a02135330325a6c379c3e334c2d6c0eff67deea6afe8d1ae799a1b/687474703a2f2f617574616e2e61382e776f6233382e61726368616d2e64653a32383038302f6275696c645374617475732f69636f6e3f6a6f623d4d696e696d616c4578616d706c6573253246476974487562576562686f6f6b4578616d706c65)

# webhooktest

## Init

### 1. Jenkins Setup:

#### Prerequisites:

- Jenkins instance up and running.
- [GitHub plugin](https://plugins.jenkins.io/github/) installed on Jenkins.

#### Configuration:

1. **Create a New Job**:
   - Navigate to the Jenkins dashboard.
   - Click on "New Item".
   - Name your project (e.g., "GitHubWebhookExample").
   - Choose "Freestyle project" and click "OK".

2. **Source Code Management**:
   - Under "Source Code Management", choose "Git".
   - Enter the Repository URL of your GitHub repo.
   - If your repo is private, you'll need to set up authentication.

3. **Build Triggers**:
   - Under "Build Triggers", select "GitHub hook trigger for GITScm polling".

4. **Build**:
   - As a simple example, in the "Build" section, add an "Execute shell" step with the command:
     ```bash
     echo "Build triggered by GitHub webhook!"
     ```

5. **Save the Job**.

### 2. GitHub Setup:

1. **Get Jenkins External URL**:
   - Your Jenkins instance must be accessible from the internet for GitHub to send it webhook requests.
   - If your Jenkins is behind a firewall or on a local network, you might need to use services like `ngrok` to expose it, or set up proper port forwarding and DNS resolution.

2. **Create Webhook**:
   - Go to your GitHub repository.
   - Click on "Settings" → "Webhooks" → "Add webhook".
   - For "Payload URL", enter your Jenkins URL followed by `/github-webhook/`. For instance:
     ```
     http://your.jenkins.server/github-webhook/
     ```
   - Set the "Content type" to `application/json`.
   - Choose the events you want to trigger the build. For starters, you can just choose "Just the push event".
   - Finish by clicking "Add webhook".

### 3. Test:

1. Make a change in your GitHub repo and push the change.
2. This should trigger the Jenkins job you set up.
3. Go to the Jenkins dashboard and check the console output of the job run. You should see the message "Build triggered by GitHub webhook!".
**Security Note**: Exposing Jenkins to the public internet can have security implications. Ensure you have secured Jenkins appropriately, using measures like:
- Changing the default admin username/password.
- Ensuring that Jenkins runs over HTTPS.
- Setting up proper authentication and authorization.
- Using a firewall to restrict incoming connections to specific IP addresses or IP ranges (like those from GitHub).

