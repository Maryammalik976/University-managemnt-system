# University-managemnt-system



Skip to content
Using Gmail with screen readers
dbms 
Meet
Hangouts

Fwd: Dbms project
Inbox

Afaq Rashid <afaqrashid4421@gmail.com>
Attachments
Thu, 4 Jun 2020, 13:45
to me

   
Translate message
Turn off for: English

---------- Forwarded message ---------
From: Faisal Muhammad <faisimehar21@gmail.com>
Date: Thu, 4 Jun 2020, 2:30 pm
Subject: Fwd: Dbms project
To: afaqrashid4421 <afaqrashid4421@gmail.com>



---------- Forwarded message ---------
From: Haider sarfraz <haidersarfraz56@gmail.com>
Date: Thu, Jun 4, 2020, 2:28 PM
Subject: Dbms project
To: Faisal Mehar <faisimehar21@gmail.com>



2 Attachments
create database projectclass;
use projectclass;
create table university(uni_name varchar(30) primary key, reg_no decimal unique,uni_address varchar(50));
create table department (dept_id int primary key, dept_name varchar(30),uni_name varchar(30) foreign key references university);
create table faculty (fac_id int primary key,designation varchar(20), fac_name varchar(30),dept_id int foreign key references department,
std_id int foreign key references student,fac_cell numeric, fac_email varchar(30),fac_address varchar(40));
create table program (program_id int primary key, prog_name varchar (20), dept_id int foreign key references department,
std_id int foreign key references student);
create table course (std_id int foreign key references student, rate_course int,course_id int, course_name varchar(20)  primary key,
program_id int foreign key references program);
create table student(uni_name varchar(30) foreign key references university, std_id int primary key, std_name varchar(30),
std_address varchar(60), std_cell numeric, std_email varchar(20));
create table administrative (admin_id int primary key, admin_name varchar(20),uni_name varchar(30) foreign key references university);
create table securitys(security_id int primary key,security_name varchar(20), admin_id int foreign key references administrative);
create table section(strength decimal,sess varchar(20), program_id int foreign key references program,sec_name varchar(20),std_id
int foreign key references student);
create table registration(reg_id int, reg_name varchar(50),admin_id int foreign key references administrative);

insert into university
values
('Badar University',123,'47-C Civic Center Airport lahore');


insert into department
values
(10,'Computer Sceince','Badar University'),(11,'Management Sceince','Badar University'),(12,'Professional Pyschology','Badar University');


insert into faculty 
values
(1,'Lecturer','Junaid',10,008,12345689,'badar@gmail.com','Lahore airport');

insert into faculty 
values
(2,'Lecturer','Fayyaz',10,008,0987654,'fayyaz@gmail.com','Gardern Town'),
(3,'Jr.Lecturer','Basit',10,008,12344,'kahn@gmail.com','Johar Town');
select * from faculty;

insert into program
values
(2,'BSCS',10,008);

insert into program
values
(3,'BSIT',10,009);

insert into course
values
(008,3720,235,'DSA',2),
(008,3720,240,'OOP',2),
(008,3720,241,'MVC',2);


insert into administrative values (30,'mirza','Badar University');
insert into securitys values (100,'Amjad',30);
select * from student;

insert into student
values
('Badar University',009,'Fahad','Model Town',12345,'fahad@gmail.com')
,('Badar University',021,'Mirza','Garden Town',123456,'mirza@gmail.com'),
('Badar University',018,'Faisal','Garden Town',2345,'faisal@gmail.com'),
('Badar University',024,'Zaid','Johar Town',456,'zaid@gmail.com'),
('Badar University',0088,'Badr','WapdaTown',1234,'haider@gmail.com');


insert into section values (40,'Spring-2019',2,'A',008);
insert into registration values (53,'registration name',30);





--views
create view stu_fac
as
select *  from student 
left join faculty
on
student.std_id=faculty.fac_id;

--view
create view stu_dept
as
select * from student 
full join department
on
student.std_id=department.dept_id;

--view
create view dept_fac
as
select * from faculty full join department
on
faculty.fac_id=department.dept_id;



--1 count number of students
select std_name,count(std_id) 'number of students' from student;

--2 student join with course
select std_name from student full join course on student.std_id=course.course_id;



--3 student join with programs
select std_name from student full join program on student.std_id=program.program_id;

--4 faculty join with course
select fac_name from faculty full join course on faculty.fac_id=course.course_id;

--5 count number of students in faculty table
select std_name from student 
where
std_id in
(select std_id,count(std_id)fac_name from faculty group by fac_name);

--6 count faculty
select fac_name,count(fac_name) from faculty group by fac_name;

--7 count deparrtment of university
select dept_name,count(dept_name) from department group by dept_name;

--8 name of department where id is=""
select dep_name,count(dep_name) from department group by dept_name having dept_id = 10;

--9 student join sections
select std_name from student full join section on student.std_id=section.sec_name;

--10 count student name from section
select std_name,count(std_name) from student full join section on student.std_id=section.sec_name;

--11 faculty join department
select fac_name from faculty inner join department on faculty.fac_id=department.dept_id;

--12 department join with university
select dept_name from department inner join university on department.dept_id=university.uni_name;

--13 count department name 
select dept_name,count(dept_name) as 'count deptpartment' from department inner join university on department.dept_id=university.uni_name
group by dept_name;

--14 section join with course
select sec_name from section full join course on section.sec_name=course.course_id;

--15 section name count and join with course
select sec_name,count(sec_name) as 'no of section' from section full join course on section.sec_name=course.course_id;

--16 administration join with securtiy
select admin_name from administrative inner join securitys on administrative.admin_id=securitys.security_id;

--17 registartion name join with administration
select reg_name from registration left join administrative on registration.reg_id=administrative.admin_id;

--18 registration count with administartion
select reg_name,count(reg_name) from registration left join administrative on registration.reg_id=administrative.admin_id
group by reg_name;


--19 delete a student
delete from student
where std_id = 008;

--20 add a column
alter table student
add email varchar(50);

--21 drop a column
alter table student
drop column email;

--22 delete the table data
truncate table student;

--23 drop the table
drop table student;


--24 update the column
update student
set email = 'fabalam5@gmail.com'
where std_id = 008;

--25 select name that start with b
select std_name from student where std_name like 'b%';

--26 display string that contain three letters
select SUBSTRING
(std_name,1,3) as 'substring' from student;

--27 display the name in lower formats
select lower
(std_name) from student;

--28 display the name in upper formats
select upper
(std_name) from student;

--29 display the distinct name
select distinct * from student;

--30 display the student detail result
select concat
(std_id,'with'std_name)
as 'STUDENT_DETAIL'
from student;;



---procedure
--1
create procedure student_name
as
select std_name from student inner join department on student.std_id=department.dept_id;
GO;
exec student_name;
--2
create procedure department_name
as
select dept_name from department inner join university on department.dept_id=university.reg_no;
GO;
exec department_name;
--3
create procedure program_names
as
select prog_name from program inner join department on program.program_id=department.dept_id;
GO;
exec program_names;
--procedure one parameter

create procedure student_work
@std_name varchar(50)
as
select * from student
where std_name=@std_name;
GO;

exec student_work
std_name = "Arsal";

--procedure with multiple parameter
create procedure student_data
@std_name varchar(50),@uni_name varchar(50)
as
select * from student 
where std_name = @std_name and uni_name = @uni_name
GO;

exec student_data
std_name = "Arsal",uni_name="Badar University";

-




---transaction
begin tran
insert into student
values
('Badar University',048,'Arsal','Model Town',12345,'arsal@gmail.com');
select * from student where std_name='Arsal'
rollback transaction
select * from student where std_name='Arsal'
labproject.sql
Page 2 of 2
