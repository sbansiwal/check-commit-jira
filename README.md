# Find Jira Issue

<p>The workflow file is located at <strong>.github/workflows/main.yml</strong></p>

<p>There is 1 job running in this workflow file which is <strong>"Find Issue Key"</strong></p>

<p>There are 3 steps in this job:</p>

<ol>
   <li>Checkout</li>
   <li>Login</li>
   <li>Get Issue Key</li>
</ol>

<p>Each of these steps uses an action code for execution</p>

<p>The steps are explained as under:</p>
<ol>
   <li><h2>Checkout</h2>
   <p>Action code ref - actions/checkout@master<br />
   This action checks-out your repository under $GIT HUB_WORKSPACE, so your workflow can access it<br />
   </p>
   </li>   
   
  <li><h2>Login</h2>
   <p>Action code ref - atlassian/gajira-login@master<br />
   Used to store credentials for later use by other Jira Actions<br />
   
   <h3>Action Spec:</h3> </br>
   
   <h4>Enviroment variables:</h4>
   JIRA_BASE_URL - URL of Jira instance. Example: https://<yourdomain>.atlassian.net<br />
   JIRA_API_TOKEN - Access Token for Authorization. Example: HXe8DGg1iJd2AopzyxkFB7F2 (How To)<br />
   JIRA_USER_EMAIL - email of the user for which Access Token was created for . Example: human@example.com<br />

   <h4>Arguments:</h4>
   None<br />

   <h4>Writes fields to config file at $HOME/jira/config.yml</h4>
   email - user email<br />
   token - api token<br />
   baseUrl - URL for Jira instance<br />

   <h4>Writes fields to CLI config file at $HOME/.jira.d/config.yml</h4>
   endpoint - URL for Jira instance<br />
   login - user email<br />

   <h4>Writes env to file at $HOME/.jira.d/credentials</h4>
   JIRA_API_TOKEN - Jira API token to use with CLI<br /></p>
   </li>
  
 <li><h2>Get Issue Key</h2>
   <p>Action code ref - sunil-bansiwal/find-jira-issue@master<br />
   Finds Jira issue key from the commit message in the Pull request<br />
   
   <h4>Cases when this step fails the workflow:</h4>
   - When the Jira issue key does not exist in the commit message<br />
   - When the Jira issue key is invalid<br />
   - When the Jira issue is marked as "Done" in the Jira account<br />
   
   If the commit message does not fall under the above given cases, the workflow (checker) is passed and the developer can        create a Pull request else he won't be able to unless he is the admin of the repo.<br />
   
   <h3>Action Spec:</h3>
   
   <h4>Environment variables</h4>
   None
   
   <h4>Inputs</h4>
   from - Find from predefined place (should be either 'branch', or 'commits', default is 'commits')<br />

   <h4>Outputs</h4>
   issue - Key of the found issue<br />
   status - Status of the issue<br />
   
   <h4>Reads fields from config file at $HOME/jira/config.yml</h4>
   None<br />

   <h4>Writes fields to config file at $HOME/jira/config.yml</h4>
   issue - a key of a found issue<br />
   
   <h4>Writes fields to CLI config file at $HOME/.jira.d/config.yml</h4>
   issue - a key of a found issue<br />
   </p>
   </li>
  
