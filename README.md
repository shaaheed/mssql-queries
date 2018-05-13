# mssql-queries

#### Table of  contents

<ul>
	<li>
		<a>Database</a>
		<ul>
			<li>
				<a href="#cerate-database">Create Database</a>
				<a href="#rename-database">Rename Database</a>
				<a href="#rename-database">Rename Database Using Stored Procedure</a>
			</li>
		</ul>
	</li>
</ul>

###### <span id="#cerate-databases">Create Database</span>
```sql
create database test
```

###### <a id="#rename-database">Rename Database</a>
```sql
alter database test modify name = test2
```

###### <a id="#rename-database">Rename Database Using Stored Procedure</a>
```sql
exec sp_renameDB 'test2', 'test3'
```

###### <a id="#drop-database">Drop Database</a>
```sql
drop database test3
```

###### <a id="#change-single-mode">Change Single Mode</a>
```sql
-- if another user is using dropped database
-- then need to change database mode to single user mode
alter database test3 set single_user with rollback immediate
```
###### <a id="#create-table">Create Table</a>
```sql
create table Person (
	Id int not null primary key,
	Name nvarchar(50) not null,
	Email nvarchar(50) not null,
	GenderId int null
)

create table Gender (
	Id int not null primary key,
	Gender nvarchar(50) not null
)
```

###### <a id="#add-column">Add Column</a>
```sql
alter table Person add Address nvarchar(50) null
```

###### <a id="#drop-column">Drop Column</a>
```sql
alter table Person drop column Address
```

###### <a id="#add-foreign-key-constraint">Add Foreign Key Constraint</a>
```sql
alter table Person add constraint FK_Person_GenderId_Gender_Id foreign key (GenderId) references Gender (Id)
```

###### <a id="#add-default-constraint-into-existing-column">Add Default Constraint Into Existing Column</a>
```sql
alter table Person add constraint DF_Person_GenderId default 3 for GenderId
```

###### <a id="#add-default-constraint-into-new-column">Add Default Constraint Into New Column</a>
```sql
alter table Person add GenderId2 int null constraint DF_Person_GenderId2 default 3
```

###### <a id="#add-check-constraint">Add Check Constraint</a>
```sql
alter table Person add constraint CH_Person_Age check (Age > 0 and Age < 100)
```

###### <a id="#drop-constraint">Drop Constraint</a>
```sql
alter table Person drop constraint FK_Person_GenderId_Gender_Id
alter table Person drop constraint DF_Person_GenderId
alter table Person drop constraint CH_Person_Age
```

###### <a id="#insert-values">Insert Values</a>
```sql
insert into Gender (Id, Gender) values (1, 'Male'), (2, 'Female'), (3, 'Unknown')
insert into Person (Id, Name, Email, GenderId) values (1, 'A', 'a@a.com', 1), (2, 'B', 'b@b.com', 2)
insert into Person (Id, Name, Email) values (3, 'C', 'c@c.com')
```
