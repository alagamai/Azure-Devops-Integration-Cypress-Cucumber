# Azure Pipeline Devops integration with Cypress + Cucumber  

# Step by Step Guide To Run / Set-Up Cypress Tests in Azure DevOps Pipeline CI/CD
# Prerequisites
1.	You need to have already cypress framework up and running on your local machine
2.	Cypress Project should be checked into the repository with visibility set to private 
3.	Your framework should generate a cucumber report 

Step 1:  Create a Github service connection 
Select github
Select project -> Project settings -> New  service connection -> search for Github -> click on next -> select Oauth configuration -> Azure pipelines
Click on authorize
Or connect using PAT 
How to generate token with github
a.	Go to profile -> settings -> Developer settings
b.	Personal access token -> token (classic)
c.	New personal access token (classic)
d.	Repository access – public repo 
e.	Generate token 
f.	Copy token  
Go to project settings ->.Github connection -> link private repo 
Confirm access 
select repository access
Approve and installi

Step 2: Create a New Pipeline
Go to  https://dev.azure.com/
Create your new pipeline. Navigate to Azure DevOps > From your Azure DevOps home page, Hover on Pipelines and Click on Pipelines
Click on the new pipeline 

Step 3: Click on Use the Classic Editor
Step 4: Choose the Correct Repository and Project
Select empty pipeline
Select Agent specification as – macos-latest

Step 5: Add powershell script
Select powershell script path  or add inline script
Add webhook url into the script 
Write your PowerShell commands here.

	Write-Host "Hello World"

	$webhookUrl = "https://hooks.slack.com/services/T05AF19455"  # Replace with your Slack webhook URL
$message = "Build Started"

	$body = @{
    	text = $message
	}
	Invoke-RestMethod -Uri $webhookUrl -Method Post -Body ($body | ConvertTo-Json)

step 6: To configure a Slack webhook URL, follow these steps:
1.	Sign in to your Slack workspace (or create a new one if you don't have an account).
2.	Once you're signed in, navigate to the Slack App Directory at https://slack.com/apps.
3.	In the search bar, type "Incoming Webhooks" and select the "Incoming Webhooks" app from the results.
4.	Click on the "Add to Slack" button to install the Incoming Webhooks app to your workspace.
5.	Select the channel where you want to receive the webhook messages and click on the "Allow" button.
6.	On the next page, you'll see a section titled "Webhook URL." Copy the URL provided in that section.
Note: The webhook URL is unique to your Slack workspace and channel. Make sure not to share it publicly or expose it in any insecure manner.
7.	Now, you can use the copied webhook URL in your Cypress tests or any other application to send messages to Slack. Replace 'YOUR_WEBHOOK_URL' with the copied URL.
Here's an example of how the webhook URL looks:
8.	https://hooks.slack.com/services/T05AF9UXXXXXXXXXXXX55

step 7: add npm package and install cypress dependencies 
Click on agent job1 + 
Search for npm 
add npm and select command install

step 8: Add another npm package to execute custom command -  npm run test script 
step 9: Add the package – cucucmber html report 

step 10: Add slack notification task 
Here are the steps to generate a Slack API token by creating a Slack app:
https://github.com/kasunkv/slack-notification/blob/master/generate-slack-token.md

step 11: to run piepline 
Click on save and queue -> to save and run

 
 # Screenshots
[![Classic-Editor](https://github.com/alagamai/Azure-Devops-Integration-Cypress-Cucumber/blob/master/images/Classic-editor-Agent-Job.png)]
[![Publish-Artifacts](https://github.com/alagamai/Azure-Devops-Integration-Cypress-Cucumber/blob/master/images/Publish-Artifacts.png)]
[![Slack-Notification](https://github.com/alagamai/Azure-Devops-Integration-Cypress-Cucumber/blob/master/images/Slack-Notification.png)]
[![classic-editor-pipeline-script](https://github.com/alagamai/Azure-Devops-Integration-Cypress-Cucumber/blob/master/images/classic-editor-pipeline-script.png)]
[![cucumber-report](https://github.com/alagamai/Azure-Devops-Integration-Cypress-Cucumber/blob/master/images/cucumber-report.png)]
