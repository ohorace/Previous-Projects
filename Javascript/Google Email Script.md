```javascript
//Created September 11th, 2018
//Sends out birthday emails
//Runs every morning around 8am and sends error messages (if any) around 9am
//Uses 'Birthday_Emails' spreadsheet


function sendBirthdayEmails() {
  //gets spreadsheet ID then sets and gets data range (all values in spreadsheet)
  //NOTE: ID is used instead of 'active sheet' because this runs automatically
  var spreadSheet = SpreadsheetApp.openById('**omitted**');
  var dataRange = spreadSheet.getDataRange();
  var data = dataRange.getValues();
  
  //get the value of today's date
  var today = new Date();
  today.setHours(0,0,0,0);
  
  //get picture using ID and set picture name
  var birthdayPicture = DriveApp.getFileById('**omitted**').getBlob().setName("birthdayPicture");
  
  //Loop through data in spreadsheet
  for (var i = 1; i < data.length; i++) {
    (function(val) {
      //collect row of data, define name, email, and birthday
      var row = data[i];
      var name = row[0]; 
      var emailAddress = row[1]; 
      var dateField = row[2];
      
      //log date field for debugging purposes
      Logger.log('Date: ' + dateField);
      
      //check to make sure no fields are blank
      if((name != '') && (emailAddress != '') && (dateField !=  '')){
        //check if their birthday is today
        if(dateField.getMonth() == today.getMonth() && dateField.getDate() == today.getDate()) {
          //set message field and subject line
          var subject = 'Happy Birthday!';
          var message = '';
        
          //send email with inline image
          GmailApp.sendEmail(emailAddress, subject, message, {
            htmlBody:'Dear ' + name + '\n\n' + '<img src = "cid:image">',
            inlineImages: {image: birthdayPicture}
          });
        }
      }
      })(i);
   }
}
```
