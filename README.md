[![Build Status](http://autan.a8.wob38.archam.de:28080/buildStatus/icon?job=MinimalExamples%2FGitHubWebhookExample)](http://autan:28080/job/MinimalExamples/job/GitHubWebhookExample/)

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
