GOALKEEP ROI MAPPER — NEW WEBSITE SYSTEM
=========================================

FILES
-----
1. Goalkeep_ROI_Website_New_Code.gs
   Fresh Google Apps Script backend. It creates a new multi-client response workbook.

2. Goalkeep_ROI_Website_New_index.html
   Fresh client-facing website for GitHub Pages or another static host.


PART A — CREATE THE NEW BACKEND
-------------------------------

1. Go to script.google.com.
2. Create a NEW Apps Script project.
3. Rename it, for example: Goalkeep ROI Website Backend.
4. Delete the default myFunction code.
5. Paste the complete contents of Goalkeep_ROI_Website_New_Code.gs into Code.gs.
6. Save.
7. From the function dropdown, select:

   createGoalkeepROIWebsiteSystem

8. Click Run and grant permissions.
9. Open Execution log. It will show the URL of the new response workbook.
10. Open that workbook and confirm these tabs exist:

   1. Client Index
   2. Rating
   3. Baseline
   4. Endline
   5. Raw Submissions
   6. Question Catalogue

Do not run createGoalkeepROIWebsiteSystem again in the same project.
To reopen the workbook link later, run:

   showGoalkeepROIWebsiteSystemLinks


PART B — DEPLOY THE APPS SCRIPT WEB APP
---------------------------------------

1. In Apps Script, click Deploy > New deployment.
2. Select type: Web app.
3. Execute as: Me.
4. Who has access: Anyone.
5. Click Deploy.
6. Copy the Web App URL ending in /exec.
7. Test the URL in an Incognito window. It should show a JSON message saying the backend is live.


PART C — CONNECT THE WEBSITE
----------------------------

1. Open Goalkeep_ROI_Website_New_index.html in a text editor.
2. Find this line:

   const SHEET_URL = 'PASTE_YOUR_APPS_SCRIPT_WEB_APP_URL_HERE';

3. Replace the placeholder with the /exec Web App URL copied above.
4. Save the file.


PART D — DEPLOY AS A NEW GITHUB PAGES SITE
------------------------------------------

1. Create a new GitHub repository, for example:

   goalkeep-roi-mapper-v2

2. Rename Goalkeep_ROI_Website_New_index.html to index.html.
3. Upload index.html to the repository root.
4. Open repository Settings > Pages.
5. Under Build and deployment, choose:

   Deploy from a branch
   Branch: main
   Folder: /root

6. Save and wait for the new website URL.
7. Open it in an Incognito window for testing.


HOW THE WEBSITE WORKS
---------------------

BASELINE
1. Client selects Baseline.
2. Client enters organisation, engagement/project, respondent and date.
3. Client completes all 1–5 rating questions on Page 1.
4. Client selects relevant metrics on Page 2.
5. Client enters Baseline values on Page 3.
6. After the backend confirms the save, the website displays a unique Engagement ID.

ENDLINE
1. Client selects Endline.
2. Client enters the Engagement ID and clicks Load Baseline.
3. The website loads the organisation, project, Baseline ratings, reasons, selected metrics, values and units.
4. Baseline ratings appear beside the Endline rating questions on Page 1.
5. The client does not reselect metrics on Page 2.
6. Baseline values appear as read-only references on Page 3.
7. Client enters current values, evidence, monetisation details, Goalkeep attribution, permission and examples.
8. Endline results are saved against the same Engagement ID.


ATTRIBUTION BUCKETS
-------------------

Low contribution — 0% to 24%       Calculation rate: 12%
Medium contribution — 25% to 49%   Calculation rate: 37%
High contribution — 50% to 74%     Calculation rate: 62%
Very high contribution — 75% to 100% Calculation rate: 87.5%

A default deadweight rate of 20% is retained in the Endline table.


IMPORTANT RELIABILITY IMPROVEMENT
---------------------------------

The website sends the response to Apps Script and then checks the Raw Submissions tab using a unique Client Submission ID. It shows the final success page only after the backend confirms that the response was actually saved.

This prevents the earlier problem where a no-cors request could show “Submitted” even when the Sheet had not been updated.


TEST BEFORE SHARING
-------------------

1. Submit one test Baseline.
2. Confirm rows appear in Client Index, Rating, Baseline and Raw Submissions.
3. Copy the displayed Engagement ID.
4. Start an Endline response and load that ID.
5. Confirm Baseline ratings and metric values appear.
6. Submit Endline.
7. Confirm Rating rows update and Endline rows contain calculations, evidence, attribution and permissions.


WHEN APPS SCRIPT CODE IS UPDATED LATER
--------------------------------------

Save the code, then go to:
Deploy > Manage deployments > Edit > New version > Deploy

The Web App URL normally remains the same when the existing deployment is updated.
