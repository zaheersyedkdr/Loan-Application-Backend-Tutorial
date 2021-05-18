# Loan-Application-Backend-Tutorial
Project for students to learn and practice API development skills


Objective :
  a. Provide API specifications and design of a loan processing application
  b. provide test suite to run and check correctness


Project Overview : Basic loan application processing application. It serves two types of users - Applicant, Officer

Applicant :
  1. Register / Login - Authentication/Authorization
  2. Apply for loan by filling all details
  3. View status of loan

Officer :
  1. View all applications of different stages
  2. Move applications to different stages
  3. Approve/Reject applications
  4. Get statics over a period of time\
  5. Create/View/Edit/Delete different loan types



Additionally there is a party called Bureau that supplies financials of applicant.
For this project a Bureau is bundled. You can use it for interactions with the Bureau.

We only concentrate creating APIs, no UI involved. It is assumed all operations in the below flow will be done via APIs.


Loan application flow :

  1. Applicant registers on loan portal and gets credentials
  2. Applicant submits loan application using the credentials received
  3. The server runs pre-defined checks as per loan type set by Officer
  4. if the checks pass - the Application moves to "NEW" state.
  5. Otherwise the application is moved to "INVALID" and user notified in response
  6. Officer sees the "NEW" applications and checks for any evident fakes.
  7. If officer detects any fraudulent/fake applications , Officer can Reject the application.
     And Application moves o "REJECTED" state.
  8. If officer is okay with the details of application he/she moves the application to "INITIATED" state.
  9. Officer initiates Bureau details fetch for applications. He/She can do it for individual applications or in bulk mode.
  10. After receiving Bureau details, the application automatically moves to "REVIEW" state.
      Bureau details are added to applications.
  11. Officer can view all "REVIEW" applications. And based on Bureau details officer can reject or approve application.
  12. Based on officer's action the state of application moves to "REJECTED" or "APPROVED"
  13. Applicant can view status of application all through the process.


APIs :

 1. Applicant Registration -  POST "/api/register"

     Authentication : NONE

     Request body :
          {
             "FirstName" : "Zaheer",
             "LastName" : "Basha",
             "Username" : "zsb"
          }
     Response :

      200 OK : if username does not exist.
      409 CONFLICT : if username already exists.
      500 : for other errors

      response body :
        {
          "success" : true/false
          "message" : "successful/error message"
        }

 2. Submit loan application - POST "api/loan/apply"

       Authentication : TOKEN

 3. Status of loan application - GET "/api/loan/{id}/status"

 4. Officer - fetch applications by state - GET "/api/loan/get/{state}"

 5. Officer - get application details - GET "/api/loan/{id}"

 6. Officer - fetch Bureau details - POST "/api/loan/bureau"

 7. Officer - Change state of application - POST "/api/loan/{id}/state"

 8. Officer - Create new loan type - POST "/api/loantype"

 9. Officer - Get loan type -GET - "/api/loantype/{typeId}"

 10. Officer - Delete loan type - DELETE - "/api/loantype/{typeId}"

 11. Officer - Edit loan type - PUT - "/api/loantype/{typeId}"
