# 01_Intro Screen

## Main elements

### Central section 
- two buttons activating radio buttons:
    - Approvals - btnApprovals
    - Operations - btnOperations
- radio buttons for Approvals - rdoApprovals
- radtio buttons for Operations - rdoOperations

Their scope is to choose type of the operation by user

### Continue button
btnContinue navigates to screen based on user selection in cetnral section. It creates collections to be displayed in galeries on other screens and user variables:
- gblUserHomeORg - user home organisation
- gblUserDis - user discipline
- colPeopleForApproval_HomeOrg - PAFs with level 0
- colPeopleForApproval - colPeopleForApproval_HomeOrg filtrated with user project
- colNewStartersPM_HomeOrg - PAFs with level 2
- colNewStartersDM_HomeOrg - PAFs with level 3
- colNewStartersPM - colNewStartersPM_HomeOrg filtrated with user project
- colNewStartersDM - colNewStartersDM_HomeOrg filtrated with user project

### Full CSV Export
btnFull export runs the flow flwCreateCSVwithHistory, that sends the full SMA_AT5 table with two archival records to the users email. 

### View Rejected
btnRejected opens up pupRejcted

### Top bar
Contains buttons navigating to [01_Intro](01_Intro.md), [05_Help](05_Help.md), [06_Contact](06_Contact.md), [07_Admin](07_Admin.md). The search window in the center of the bar activates galApprovalStatus, showing the current status of serached person. In the right corner email and picture of the user is displayed. 




