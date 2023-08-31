# Offboarding

### How to offboard a PAF?
Offboarding function is available for Project Controllers.

How to offboard a PAF?
1. Select Partner Project Controller -> Edit Existing PAFs
2. Select Home Organisation in filters pane (necessary to see a gallery) 
3. Select a PAF
4. Click 'Offboard'
5. Click 'Apply changes'

   flowchart LR
    A(Offboard button clicked) --> B[Set:\nLevel_calc = 99\nEditComment = 'Offboarding'\nEndDate=<i>Now</i>\nLastEditor = <i>currentUserEmail</i>]
    B --> C[Run flwOffboardingEmail_01]
    C --> D[Run flwOffboardingSupportEmail]

### How to see offboarded PAFs?
How to offboard a PAF?
1. Choose Partner Project Controller -> Edit Existing PAFs
2. Turn on 'Offboarded' filter
3. Select Home Organisation

## Database flow
