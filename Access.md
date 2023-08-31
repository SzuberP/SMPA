# Access to the Onboarding Portal

To give a users access to the Onboarding Portal the following actions are required:

### 1. Add a user to the [dbo].[People] table:

```rb
-- INSERT NEW ROW INTO PEOPLE
INSERT INTO [dbo].[People] ([Group],[GroupID],[Name],[Email],[Home_organisation],[Project], [PowerUser])		
VALUES  ('PM/Workstream lead',1,'Martin Spinner','user@smpalliance.co.uk','All','All', 0) 
```

### 2. Create a new user for security
```rb
-- ADD NEW USER TO SECURITY 
CREATE USER [user@smpalliance.co.uk] FROM EXTERNAL PROVIDER 
GO
```

### 3. Add a security role
```rb
EXEC sp_addrolemember apps_ManagerDirector, 'martin.spinner@smpalliance.co.uk' 
GO 
```


