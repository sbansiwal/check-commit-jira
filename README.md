<p>The workflow file is located at <strong>.github/workflows/main.yml</strong></p>

<p>There is 1 job running in this workflow file which is <strong>"Find Issue Key"</strong></p>

<p>There are 3 steps in this job:</p>

<ol>
   <li>Checkout</li>
   <li>Login</li>
   <li>Get Issue Key</li>
</ol>

<p>Each of these steps uses an action code for execution</p>

<p>The steps are explained as under</p>:
<ol>
   <li><p>Checkout</p>
   <p>Action code ref - actions/checkout@master<br />
   This action checks-out your repository under $GIT HUB_WORKSPACE, so your workflow can access it<br />
   </p>
   </li>   
</ol>   
   
2) Login
   Action code ref - atlassian/gajira-login@master
   Used to store credentials for later use by other Jira Actions

   Action Spec:
   
   Enviroment variables:
   JIRA_BASE_URL - URL of Jira instance. Example: https://<yourdomain>.atlassian.net
   JIRA_API_TOKEN - Access Token for Authorization. Example: HXe8DGg1iJd2AopzyxkFB7F2 (How To)
   JIRA_USER_EMAIL - email of the user for which Access Token was created for . Example: human@example.com

   Arguments:
   None

   Writes fields to config file at $HOME/jira/config.yml
   email - user email
   token - api token
   baseUrl - URL for Jira instance

   Writes fields to CLI config file at $HOME/.jira.d/config.yml
   endpoint - URL for Jira instance
   login - user email

   Writes env to file at $HOME/.jira.d/credentials
   JIRA_API_TOKEN - Jira API token to use with CLI
  
3) Get Issue Key
   Action code ref - sunil-bansiwal/find-jira-issue@master
   Finds Jira issue key from the commit message in the Pull request
   
   Cases when this step fails the workflow:
   - When the Jira issue key does not exist in the commit message
   - When the Jira issue key is invalid
   - When the Jira issue is marked as "Done" in the Jira account
   
   If the commit message does not fall under the above given cases, the workflow (checker) is passed and the developer can        create a Pull request else he won't be able to unless he is the admin of the repo.
   
   Action Spec:
   
   Environment variables
   None
   
   Inputs
   from - Find from predefined place (should be either 'branch', or 'commits', default is 'commits')

   Outputs
   issue - Key of the found issue
   status - Status of the issue
   
   Reads fields from config file at $HOME/jira/config.yml
   None

   Writes fields to config file at $HOME/jira/config.yml
   issue - a key of a found issue
   
   Writes fields to CLI config file at $HOME/.jira.d/config.yml
   issue - a key of a found issue
  
