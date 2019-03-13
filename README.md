# saltytrolls
## GitHub flow
Project week March 2019. Saltiest Hacker News Trolls group 1

Re: *Git Workflow*

Each project will have their own repository.

Students clone master and create a branch *No Forks!*

Work is submitted for review to the PMs or to the Team Leaders by way of Pull-Request.

https://www.notion.so/lambdaschool/Policies-and-Procedures-19e679fc1a284b668d8132dd8d7228cd

## Customer Spec

Pitch: Build an app that uses Hacker News comment data to rank commenters based on negative comment sentiment (saltiness).

MVP: App rates and ranks hacker news commenters by negativity of comment sentiment (limited to commenters who have made x number of posts). Allows users to search by username to view comments and sentiment levels of specific users.

Stretch Goal: App also displays the sentiment of individual comments by user allowing drilldown to a user view.

Dataset: https://www.kaggle.com/hacker-news/hacker-news

## ENVIRONMENT_VARIABLES

Here is where I would like each teams required environment variables stored. Since we all work on this file, I want you to clone it. Then right before you add a variable it want you to run `get pull` in this repo, to make sure you are not deleting eachothers on your local machine. Then add the variable you need, `git commit` and `git push` right away. These will go directly to master

If the environment variable is something private just enter the `NAME=` and then include a link on the next line where the user can sign up for that key. Remember to keep all secrets secret.

### AI_ENVIRONMENT

### BACKEND_ENVIRONMENT
PORT=4000

### REACT_ENVIRONMENT
REACT_APP_ROOT_URL=netlify.com/yadayada/  url = process.env.REACT_APP_ROOT_URL/bridges/

## Backend Details
https://buildweek-saltytrolls.herokuapp.com/


### `POST /api/users/register`

#### Overview

Used to register a user and ensure that user information will be saved in the server.

#### Inputs:

* **Javascript object** with the following fields:
	- `UserEmail` (string) -> _it is assumed that only validated email addresses will be sent_
	- `UserPassword` (string) -> _this will be hashed_
  
#### Success Outputs:

* `msg` (string) -> _contains a success message string_

#### Failure Outputs:

* `msg` (string) -> _contains an error object converted into a string for greater clarity in debugging_

### `POST /api/users/login`

#### Overview

Used to log in and get authentication for accessing the main functionalities of the React app.

#### Inputs:

* **Javascript object** with the following fields:
	- `UserEmail` (string)
	- `UserPassword` (string)

#### Success Outputs:

* `UserID` (string) -> _the ID of the logged in user_
* `UserEmail` (string) -> _the email address of the logged in user_
* `token` (string) -> _token string that should be used for accessing restricted endpoints_

#### Failure Outputs:

* `msg` (string) -> _contains an error object converted into a string for greater clarity in debugging_

### `GET /api/users/auth`

**This endpoint is restricted to logged in users.**

#### Overview

Used for a quick authentication check - will simply always return a success messsage on success, and fail **(with status `401`)** if token is either unsupplied or invalid.

#### Inputs:

* **Request header (Javascript object)** that should contain the token

#### Success Outputs:

* `msg` (string) -> _contains a success message string_

#### Failure Outputs:

* `msg` (string) -> _contains an error object converted into a string for greater clarity in debugging_

### `DELETE /api/users/:id`

**This endpoint is restricted to logged in users.**

#### Overview

Used to delete the current user.

#### Inputs:

* **Request header (Javascript object)** that should contain the token _(security is in place for tokens that do not correspond to the current user being requested for deletion - **status `403` (Forbidden)** will be returned if this is attempted)_

#### Success Outputs:

* `msg` (string) -> _contains a success message string_

#### Failure Outputs:

* `msg` (string) -> _contains an error object converted into a string for greater clarity in debugging_

### `PATCH /api/users/:id/password`

**This endpoint is restricted to logged in users.**

#### Overview

Used to update the current user's password.

#### Inputs:

* **Javascript object** with the following fields:
	- `UserPassword` (string) -> _this will be hashed_
* **Request header (Javascript object)** that should contain the token _(security is in place for tokens that do not correspond to the current user being requested for a password update - **status `403` (Forbidden)** will be returned if this is attempted)_

#### Success Outputs:

* `msg` (string) -> _contains a success message string_

#### Failure Outputs:

* `msg` (string) -> _contains an error object converted into a string for greater clarity in debugging_
