# [dbo].People

People table contains all users that have access to the Onboarding Portal.
Scope od access is determined by three columns: GroupID, Home_organisation and Project.

## Fields
<ul>
<li>Group - role name visible on start screen in the App.
</li>
<li>GroupID - groupID determines what is visible in the App.
</li>
<li>Name - SURNAME FIRSTNAME
</li>
<li>Email - case sensitive, must be set as in Azure account
</li>
<li>Authority_level - not in use
</li>
<li>View_name - not in use
</li>
<li>Home_organisation - user sees only PAFs from assigned home organisation
</li>
<li>PID - unique autogenerated ID
</li>
<li>Project - user sees only PAFs on assigned schemes. Each scheme requires a separate row
</li>
<li>Category - not in use
</li>
<li>Discipline - not in use
</li>
<li>Level_calc 
</li>
<li>PowerUser
</li>
</ul>
