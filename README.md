# Code for calling api from appsheet

var ss = SpreadsheetApp.openById("1rV2_S2q5rcakOuHs2E1iLeKR2floRIozSytAt2iRXo8");
  var sheet = ss.getSheets()[0];
  var data = sheet.getDataRange().getValues();
  var dataToImport = {};
  for(var i = 1; i < data.length; i++) {
    var firstName = data[i][0];
    var lastName = data[i][1];
    dataToImport[firstName + '-' + lastName] = {
      firstName:firstName,
      lastName:lastName,
      emailAddress:data[i][2],
      country:data[i][4],
      department:data[i][5],
      weight:data[i][6],
      birthDate:data[i][7]
    };
  }
  var firebaseUrl = "https://script-examples.firebaseio.com/";
  var base = FirebaseApp.getDatabaseByUrl(firebaseUrl);
  base.setData("", dataToImport);
