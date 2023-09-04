## Partner Project Controller
Project Controllers see all PAFs from one organisation.

#### Approve
``` mermaid
flowchart LR
    J[Database Update]
    A('Approve' button clicked) --> B{Is End Date empty?\nIs project 'Not applicable'?\nIs End Date before Start Date?\nIs Email address invalid?} 
    B --> |yes|C[Show warning window]
    C --> B
    B --> |no|H[Set approval text\nlocApprovalText=<i>ControllEmail_timestamp]
    H --> G[Show approval window]
    G --> |Apply Changes|I[Set:\nLevel_Calc=1\nControlSignoff=locApprovalText\nControlComments=<i>control comment</i>\nLastEditor=<i>currentUserEmail]
    style I fill:#CEE39D
    style J fill:#CEE39D
```

#### Reject
``` mermaid
flowchart LR
    E[Database Update]
    J[Power Automate flow trigger]
    A('Reject' button clicked) --> B[Show approval window]
    B --> C{Is 'Reason of rejection' blank?}
    C -->|No|D['Apply Changes' button active]
    D --> |Apply Changes|I[Set:\nRej_calc=1\nControlSignoff=locApprovalText\nRejected=<i>Reason of rejection</i>\nLastEditor=<i>currentUserEmail]
    I --> H[flwRejectPCEmail_01]
    style I fill:#CEE39D
    style E fill:#CEE39D
    style J fill:#94DFEE
    style H fill:#94DFEE
```

## National Highways

``` mermaid
flowchart LR
    J[Database Update]
    A('Update New Starter Form' button clicked) --> B{Reject or Approve selected?}
    B -->|Approve|C[Set approval signoff]
    B -->|Rejected|D[Set rejection signoff]
    C--> E[Show approval window]
    D--> F[Show rejection window]
    E-->|Approve|G[Set:\nLevel_calc=2\nPM_DIM_Approved=locApprovalText\nLastEditor=<i>currentUserEmail]
    F --> H{Is 'Reason of rejection' blank?}
    H -->|No|K['Reject' button active]
    K --> |Reject|I[Set:\nRej_calc=1\nPM_DIM_Approved=locRejectText\nRejected=<i>Reason of rejection</i>\nLastEditor=<i>currentUserEmail]

    style J fill:#CEE39D
    style I fill:#CEE39D
    style G fill:#CEE39D
```


## Budgetholder

``` mermaid
flowchart LR
    J[Database Update]
    A('Update New Starter Form' button clicked) --> B{Reject or Approve selected?}
    B -->|Approve|C[Set approval signoff]
    B -->|Reject|D[Set rejection signoff]
    C--> E[Show approval window]
    D--> F[Show rejection window]
    E-->|Approve|G[Set:\nLevel_calc=4\nPM_DIM_Approved=locApprovalText\nEditComment=Justification for approval\nLastEditor=<i>currentUserEmail]
    F --> H{Is 'Reason of rejection' blank?}
    H -->|No|K['Reject' button active]
    K --> P{PAF's Project = Production Hub}
    P --> |Yes|I[Set:\nLevel_Calc=3\nPM_DIM_Approved=locRejectText\nLastEditor=<i>currentUserEmail]
    P --> |No|R[Set:\nRej_calc=1\nPM_DIM_Approved=locRejectText\nLastEditor=<i>currentUserEmail]
    G --> L[flwOnboardingSupportEmail_01]
    L --> M[flwBusinessColabEmail]
    M -->N{Is ProjectWise empty?}
    N -->|No|O[flwPWTeamEmail_00]
    
    style J fill:#CEE39D
    style I fill:#CEE39D
    style G fill:#CEE39D
    style R fill:#CEE39D
    style L fill:#94DFEE
    style M fill:#94DFEE
    style O fill:#94DFEE
```

## Alliance Director
``` mermaid
flowchart LR
    J[Database Update]
    A('Update New Starter Form' button clicked) --> B{Reject or Approve selected?}
    B -->|Approve|C[Set approval signoff]
    B -->|Reject|D[Set rejection signoff]
    C--> E[Show approval window]
    D--> F[Show rejection window]
    E-->|Approve|G[Set:\nLevel_calc=4\nPM_DIM_Approved=locApprovalText\nEditComment=Justification for approval\nLastEditor=<i>currentUserEmail]
    F --> H{Is 'Reason of rejection' blank?}
    H -->|No|K['Reject' button active]
    K --> I[Set:\nRej_calc=1\nPM_DIM_Approved=locRejectText\nRejected=<i>Reason of rejection</i>\nLastEditor=<i>currentUserEmail]
    G --> L[flwOnboardingSupportEmail_01]
    L --> M[flwBusinessColabEmail]
    M -->N{Is ProjectWise empty?}
    N -->|No|O[flwPWTeamEmail_00]
    
    style J fill:#CEE39D
    style I fill:#CEE39D
    style G fill:#CEE39D
    style L fill:#94DFEE
    style M fill:#94DFEE
    style O fill:#94DFEE
```

