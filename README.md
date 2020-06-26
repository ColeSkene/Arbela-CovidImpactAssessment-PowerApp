# Arbela-CovidImpactAssessment-PowerApp
This solution consists of a Model-driven Power App, a Power BI Dashboard, and various supporting components within the CDS Solution. The solution is designed to be able to stand alone within a CDS Environment without any Dynamics 365 first party apps, or integrate semalessly within an existing Dynamics 365 CE implementation. The Power BI Dashboard exposes CDS data present in your environment and extended through the Model-driven App to highlight Covid Impact data in justoposition with Johns Hopkins Covid Data for the United States.

# Installation Instructions

## Prerequisites
	• Have access to an Office 365 User with a Power Apps license
	• Have system admin access to a target power apps environment where the solution will be deployed
	• Download the Managed Solution file "COVIDMarketImpactTools_1_0_0_1_managed"
	• Download the Power BI Dashboard file "COVID Tracker.pbix"
	• Download all Sample Data files (.xlsx)
	• Have a Bing Maps API Key
		○ For initial setup and testing, a free Basic key should suffice
	• Have Power BI Desktop installed on local machine and a Power BI License with rights to deploy PBI reports to the web

## Install
	1. Go to https://make.powerapps.com/, select your target environment, and open "Solutions"
		○ If you do not have a Power Apps license, sign up for the Power Apps Community Plan
		○ If you do not have an environment, create one through the Power Platform Admin Center
	2. From the Solutions screen, select "Import" in the Command Bar
	3. Within the Import Solution dialog, select "Choose File" and select the "COVIDMarketImpactTools_1_0_0_1_managed" file downloaded previously
	4. Proceed through the dialog window with defaults selected and initiate the solution import process
	5. When complete, there may be warnings noted, but this is ok as long as the Solution has been installed
		a. Common Warnings:
			i. Process Activation: Impact Assessment - Geocode Account Address
			ii. Localized Labels

## Activate Flows
	1. From the Solutions screen, open the COVID Market Impact Tools solution
	2. At the right side of the Command Bar, select Flow in the drop-down menu to filter the list
	3. Open the "Impact Assessment - Geocode Account Address" flow and click "Edit" in the Command Bar
		a. Add CDS, Office 365 Outlook, and Bing Maps connections to the Flow
			§ Note: the Office 365 Outlook connection will define the sender address of the error notification email
		b. In the "Send an email: Global Error Message" step (Office 365 Outlook) of the "Error Handler" Scope, specify an appropriate User, Email Address, or Distribution List in the "To" field
			§ This is the address to which automated failure notification emails will be sent
		c. When complete, Save the Flow and return to the Flow details screen
		d. Click "Turn on" in the Command Bar to activate the Flow and close the tab when activation has been confirmed

## Import Sample Data
	1. Open the COVID Market Impact Tools solution
	2. At the right side of the Command Bar, select Model-driven App in the drop-down menu to filter the list
	3. Select the "Impact Assessment App" component to open the App Designer, and click "Play" to run the Model-driven App
	4. From the Impact Assessment App, click "Sales Territories" under the Reference section of the site map on the left side of the screen
		a. Click "Import from Excel"
		b. Click "Choose File" then navigate to and select the "Impact Assessment - Sales Territories (Sample).xlsx" downloaded previously
		c. Proceed through the wizard and select "Finish Import" to initiate the import
		d. After a few seconds, refresh to find three sample Sales Territories present in the "Active Sales Territories" view
	5. Click "Industries" under the Reference section of the site map on the left side of the screen
		a. Click "Import from Excel"
		b. Click "Choose File" then navigate to and select the "Impact Assessment - Industries (Sample).xlsx" downloaded previously
		c. Proceed through the wizard and select "Finish Import" to initiate the import
		d. After a few seconds, refresh to find three sample Industries present in the "Active Industries" view
	6. Click "Business Segments" under the Reference section of the site map on the left side of the screen
		a. Click "Import from Excel"
		b. Click "Choose File" then navigate to and select the "Impact Assessment - Business Segments (Sample).xlsx" downloaded previously
		c. Proceed through the wizard and select "Finish Import" to initiate the import
		d. After a few seconds, refresh to find three sample Business Segments present in the "Active Business Segments" view
	7. Click "Accounts" under the Core section of the site map on the left side of the screen
		a. Click "Import from Excel"
		b. Click "Choose File" then navigate to and select the "Impact Assessment - Accounts (Sample).xlsx" downloaded previously
		c. Proceed through the wizard and select "Finish Import" to initiate the import
		d. After a few seconds, refresh to find 27 sample Accounts present in the "Accounts (Impact Assessment)" view

## Deploy Power BI Dashboard
	1. Copy your Org URL: From anywhere in the Impact Assessment App copy the first portion of the URL from "https://" to ".com/"
		○ Example: https://mycdsorg.crm.dynamics.com/
	2. Open the previously downloaded "COVID Tracker.pbix" in Power BI Desktop
	3. Click on Transform to go to the Power Query Editor
	4. On the Left under queries click on Account
		a. On the right under Applied Steps click on the gear to the right of “Source”
		b. Within the dialog window:
			i. Paste the previously copied Org URL into the Server URL text box
			ii. Click OK
		c. You will be asked to sign in, sign in with appropriate account
		d. Click the Connect button after you have been authenticated
		e. After a few seconds, you should see the data grid come up, indicating that the Account query has been configured
		f. Click on the last item in the "Applied Steps" list to see the transformed Account dataset and confirm that the previously imported Sample Data is visible
	5. Click on BusinessSegment repeat the same steps with this query, you will not be asked to sign in again, just click Ok to connect
		a. Click on the last item in the "Applied Steps" list to see the transformed Business Segment dataset and confirm that the previously imported Sample Data is visible
	6. Repeat process for Industry, click OK to Connect
	7. Click on the COVID19 query
		a. Click on the gear Icon next to Source under the Applied Steps
		b. You will be shown a dialog “Comma-Separated Values” with a URL and other options. Leave them as they are, and click OK
		c. The Next dialog is the “Access Web Content”, you will be accessing this URL anonymously, click the Connect button. 
			i. The Yellow warning sign should disappear from the COVID19 query after navigating to another query and back
	8. Click Close & Apply in the upper Left-Hand side of the Power Query Editor to return to the Power BI Desktop Canvas with the COVID-19 Tracker Report
	9. Click on Refresh Data Icon to refresh the report
	10. Once the refresh completes, click on the Publish icon to publish the report to your Power BI Workspace
		a. Sign into Power BI as required to complete the publishing process
		b. You will need to select an appropriate workspace, for the purpose of testing, "My Workspace" will suffice
	11. Once the report has been published, click the “Open COVID Tracker.pbix” link to open the report in the Power BI Web App
	12. Copy the URL of the Dashboard from your Web Browser for use in the next task

## Edit Site Map
	1. With the URL of the previously published Covid Tracker dashboard copied to your clipboard, open the COVID Market Impact Tools solution
	2. At the right side of the Command Bar, select Other in the drop-down menu to filter the list
	3. Select the "Impact Assessment App" Site Map component to open the Sitemap Designer
		a. From the Sitemap Designer, select the "Power BI Dashboard" subarea under the "Overview" group to reveal its properties on the right
		b. From the Subarea properties pane, paste the previously copied URL into the corresponding text field
		c. At the top right of the Sitemap Designer, click Save, then Publish, then Save And Close

## Security-level Testing
	• Walk-through the various "End-to-End Scenarios" outlined in the previously downloaded Functionality Validation Guide (.docx) using a non admin user account.

## Validate Dashboard Data
	• After adding some data during Security-level Testing, confirm that this data is visible in the Covid-19 Tracker Dashboard in the following areas:
		○ Open (Count of Accounts not marked as Closed)
		○ Closed (Count of Accounts marked as Closed)
		○ %Closed (Percentage of Accounts marked as Closed from total Accounts)
		○ Top 10 Still Purchasing (Top 10 States by count of Accounts marked as Still Purchasing)
		○ Top 10 Still Open (Top 10 States by count of Accounts not marked as Closed)
		○ Top 10 Still Open (Top 10 States by count of Accounts marked as Closed)
