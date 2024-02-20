# 02_Main

Screen dedicated for:
- Partner Project Controllers approving new PAFs
- Project Accountatns
- Project Wise

## Main Elements

The screen contains main elements from the left:
- [filters pane ](#filters-pane)- filtrating PAFs gallery
- PAFs gallery - galPeopleFilters with search window (txtNameSearch)
- central details form - grpDetailsMain
- right pane with PAF edit details and approval buttons
- Mass Approval - grpMassApprval - multiple elements distributed throguh screen visible after toggling toggleMassiveApproval

Important part of the screen functionality are popup windows. Those are:
- CSV Export - pupCsvExport
- End Date set up - pupEndDate
- Home Organistation set up - pupHomeOrg
- Production Hub - pupProductionHub
- Project - pupProject
- Date - pupDate
- Reject - pupReject
- Approval - [pupApproval](#pup-approval)
- Details Edit - pupDetailsEdit

### Filters pane

Contains: 
- Mass approval toggle button (toggleMassiveApproval) turning on [mass aprroval](#mass-approval)
- Projecst radio buttons ([rdoProject](#rdoprojects)) 
- Home Organisation radio buttons ([rdoHomeOrganisation](#rdohomeorganisation))
- Discipline radio buttons ([rdoGroup](#rdogroup))
- all radio buttons can be reset with btnClearAllfilters

#### rdoProjects

Items populated with loop returning unique values of project from user projects (projectFilter).  
If user is assigned to single Home Organisation, It filters projectFilter with home organisation name. 
```rb
ForAll(Distinct(
    If(
       Text(First(gblUserHomeOrg.Result).Result) <> "All",
        Filter(
            projectFilter,
            HomeOrganisation = Text(First(gblUserHomeOrg.Result).Result)
        ),
        projectFilter
    ),
    Project
), {Result: ThisRecord.Value})
```
#### rdoHomeOrganisation

Items populated with loop returning unique values of Home organisation from colPeopleForApproval

```rb
ForAll(Distinct(
    colPeopleForApproval, 
    HomeOrganisation), 
    {Result: ThisRecord.Value})
```

#### rdoGroup

Items populated with loop returning unique values of Discipline from colPeopleForApproval

```rb
ForAll(Distinct(
    colPeopleForApproval, 
    Discipline), 
    {Result: ThisRecord.Value})
```

### Mass Approval

Mass approval is activated with toggleMassiveApproval that assign True value to **locMassiveApproval**  
Activating mass approval:
- makes check boxes (chkMassApproval) in galPeopleFilter visible
- makes Mass approval galery (galMassiveApproval) displaying PAFs with check boxes ticked in visible
- moves btnApproval lover
- makes btnMassSelectAll visible; the button checks in all checkboxes


### Pup Approval

#### Approve button (btnApproval)

Validates if PAF has correct End Date, Start Date and Email.  
If needed, it opens up popups to insert End Date or check Email. It set ups Approval text for PM_DIM_Approval field. Activates Approval PopUp 

```rb
If(
    // if
    IsBlank(cardEndDateExt.Text) || cardProject.Text="Not applicable" || DateDiff(DateValue(cardStartDate.Text),DateValue(cardEndDateExt.Text))<0 || IsBlank(cardEmail.Text) || Not("@" in cardEmail.Text) , 
    // true
    Set(EndDateMandat, true); Set(locGreyOutVis, true),
    //else
    Set(ApprovalPop_UpVis, true); Set(locGreyOutVis, true);
    Set(
    locApprovalText,
    If(
        gblUserGroupId_A = 7,
        "Approved_" & User().Email & "_" & Text(Now(), "[$-en-US]mm/dd/yyyy hh:mm:ss"),
        gblUserGroupId_A = 8,
        "Approved_" & User().Email & "_" & Text(Now(), "[$-en-US]mm/dd/yyyy hh:mm:ss"),
        gblUserGroupId_A = 9,
        "Approved_" & User().Email & "_" & Text(Now(), "[$-en-US]mm/dd/yyyy hh:mm:ss"
        )
    )
    )
);
```

### PopUp body
Contains Form (frmControl), with one editable text input crdPCComments. crd_PCSignOff is populated with text saved to locApprovalText with btnApproval. btnRejectApproval - close the PopUp.  **btnApplyEdit_1** patch changes into database. In case of mass approval it is done with a loop, otherwise with SubmitForm method. 

```rb
If(locMassiveApproval,
    //***MASSIVE APPROVAL***
    If(
        //PA
        gblUserGroupId_A = 8, ForAll(
            galMassiveApproval.AllItems,
            Patch(
                SMA_AT5,
                {ID2: ThisRecord.ID2},
                {AccountantSignoff: DataCardValue14_2.Text},
                {LastEditor: currentUserEmail}
                
            )
        ),
        //PC
        gblUserGroupId_A = 7, ForAll(
            galMassiveApproval.AllItems,
            Patch(
                SMA_AT5,
                {ID2: ThisRecord.ID2},
                {Level_Calc: 1},
                {ControlSignoff: DataCardValue14_3.Text},
                {ControlComments: DataCardValue1.Text},
                {LastEditor: currentUserEmail}
            )
        ),
        //PW
        gblUserGroupId_A = 9, ForAll(
            galMassiveApproval.AllItems,
            Patch(
                SMA_AT5,
                {ID2: ThisRecord.ID2},
                {PWAdded: DataCardValue14_4.Text},
                {PWLevel: drpPWlevel.SelectedText.Value},
                {LastEditor: currentUserEmail}
            )
        )       
    ),
    //***STANDARD APPROVAL***
    If(
        gblUserGroupId_A = 8, SubmitForm(frmCommercial),
        gblUserGroupId_A = 7, SubmitForm(frmControl),
        gblUserGroupId_A = 9, SubmitForm(frmPWAdded)
    )
);
```