# Access to the Onboarding Portal

To give a users access to the Onboarding Portal the following actions are required:

### 1. Add a user to the [dbo].[People] table:

```rb
-- INSERT NEW ROW INTO PEOPLE
INSERT INTO [dbo].[People] ([Group],[GroupID],[Name],[Email],[Home_organisation],[Project], [PowerUser])		
VALUES  ('PM/Workstream lead',1,'Martin Spinner','user@smpalliance.co.uk','All','All', 0) 
```

### 2. Create a new user for security
Only if it hasn't been done before

```rb
-- ADD NEW USER TO SECURITY 
CREATE USER [user@smpalliance.co.uk] FROM EXTERNAL PROVIDER 
GO
```

### 3. Add a security role
All existing roles have the same priviliges, so it doesn't matter which one a user has.
One database role is enough, even if a user has more than one role in the OBP.

```rb
EXEC sp_addrolemember apps_ManagerDirector, 'user@smpalliance.co.uk' 
GO 
```

### 4. Share the PowerApps app with a user

### 5. Send a ticket to IT to check if a user has been added to Azure Onboarding group


