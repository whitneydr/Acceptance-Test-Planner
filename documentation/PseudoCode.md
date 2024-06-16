# Acceptance Test Planner Pseudocode

## Registration

**DISPLAY registration form**, including input fields for email address, password and confirm password, and submit button

  **INPUT** email address  
    IF input DOES NOT INCLUDE @ symbol, DISPLAY ERROR  
    IF email address EXISTS in user data, DISPLAY ERROR

 **INPUT** password 

  **INPUT** confirm password  
  IF confirm password != password, DISPLAY ERROR

  **SUBMIT** form  
  IF fields empty or invalid, DISPLAY ERROR  
  ON SUBMIT, CREATE new entry in user database

  **DISPLAY** registration successful page

  **CLICK** Continue button  
  **DISPLAY** User dashboard
    

## Login

**DISPLAY login form**, including input fields for email address and password, submit button, and forgot password and register links

  **INPUT** email address
  IF input DOES NOT INCLUDE @ symbol, DISPLAY ERROR

  **INPUT** password
  
  **SUBMIT** form  
  IF email address EXISTS in user database  
  AND password MATCHES that user's password  
  **DISPLAY** user dashboard  

  ELSE   
  DISPLAY ERROR - "Email address or password incorrect. Reset password?"


## User dashboard

**DISPLAY navigation menu**  with current section highlighted   
>    IF pagePath CONTAINS /projects THEN "Projects" menu item active  
    ELSE IF pagePath CONTAINS /tests THEN "Tests" active  
    ELSE IF pagePath CONTAINS /reports then "Reports" active  
    ELSE IF pagePath CONTAINS /help THEN "Help and Support" active   

**DISPLAY buttons** for "Create new project" and "Create new test"

**DISPLAY main section**

> IF pagePath === /projects  
>> DISPLAY `ProjectList` component
>>> MAP projects in projects array/database 
>>>
>>>> IF filterTab !== "all", FILTER projects by filterTab [Backlog | In progress | Complete] 

>IF pagePath === /tests
>> DISPLAY `TestList` component
>>> MAP tests in Tests array/database  
>>>
>>>> IF filterTab !== "all", FILTER projects by filterTab [To do | Passed | Failed]

> IF pagePath === /reports
>> DISPLAY `Reports` component

> IF pagePath === /help
>> DISPLAY `Help` component




## Create new project

**CLICK** "Create new project" button in top navigation  

**DISPLAY project form** with input fields for:
- Project title [text][required]
- Project summary [text]
- Acceptance criteria [text]
- Due date [date]
- Priority [dropdown]
- Project owner [dropdown]

**INPUT** Project title  
IF `projectTitle` EXISTS in projects database, DISPLAY ERROR  
ELSE SAVE to project database

**INPUT** Project summary

**INPUT** Acceptance criteria  
ON "Enter" KEYDOWN,  
GENERATE Acceptance Criteria id  
ADD to Acceptance Criteria array  
ADD new input field

**INPUT** Due date

**SELECT** priority level from dropdown

**SELECT** Project owner from dropdown
> DISPLAY ProjectOwner dropdown menu
>> MAP users from user database

**SUBMIT** form 
IF projectTitle == null, DISPLAY ERROR  
ELSE SAVE entry to projects database

**CLICK** cancel button  
DROP entry from database  
DISPLAY user dashboard



## Create new test

**CLICK** "Create new test" button in top navigation

**DISPLAY test form** with input fields for:
- Project [dropdown][required]
- Test title [text][required]
- Test description [text]
- Test steps [text]
- Test data [text]
- Acceptance criteria [dropdown]
- Test type [dropdown]
- Due date [date]
- Assignee [dropdown]

**SELECT** Project from dropdown
> DISPLAY `projectList` in dropdown
>> MAP projects in projects database

**INPUT** Test title  
IF testTitle EXISTS in project, DISPLAY ERROR  
ELSE SAVE to test database

**INPUT** Test description

**INPUT** Test steps

**INPUT** Test data

**SELECT** Acceptance criteria from dropdown
> DISPLAY `acceptanceCriteria` in dropdown
>> MAP acceptanceCriteria array from project in projects database

**SELECT** test type from dropdown

**INPUT** due date

**SELECT** Assignee from dropdown

**SUBMIT** form  
IF testTitle == null, DISPLAY ERROR  
ELSE SAVE to tests database

**CLICK** cancel button  
DROP entry from database  
DISPLAY previous page



## Project page

**CLICK** project title from project list on user dashboard

**DISPLAY project page**
> DISPLAY `projectPage` component
>> GET projectID from list item
>>> FIND project in project database  
JOIN to tests in test database  
JOIN to users in user database 
>>> 
>> FETCH attributes from Database
>>

**DISPLAY report**
> DIVIDE tests.toDo by numberOfTests
>> SET width of `toDo` bar to result
>
> DIVIDE tests.passed by numberOfTests
>> SET width of `pass` bar to result
>
> DIVIDE tests.failed by numberOfTests
>> SET width of `fail` bar to result

**DISPLAY** list of tests  
> DISPLAY `testList` component
>
>> MAP tests in project
>


**CLICK** edit button  
CONVERT to input field


## Test page

**CLICK** test title from user dashboard or project page

**Display Test page**
> DISPLAY `testPage` component
>> GET testID from list item
>>> FIND test in database
>>
>> FETCH attributes from database

**INPUT** test status from dropdown  
**SAVE** to database  
**DISPLAY** Test Outcome input field  
**INPUT** details about the results of the test  
**ON SUBMIT**, SAVE to database

**INPUT** test outcome  
ON SUBMIT, SAVE to database