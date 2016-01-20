function SendTheResult() {
  var sheet = SpreadsheetApp.getActiveSheet();
  var cellref = 'AC1';
  var addtocell = 0;
  var cell = sheet.getRange(cellref);
  var value = cell.getValue();
  var newval = value.split(",");
  var arr = {};
  var newarr = {};
  for(var i=0;i<newval.length;i++) {
    newarr[newval[i]] = 1;
  }
  
  for(var k=1;k<=5;k++) {
    var url = "http://www.moneycontrol.com/news/results-27-"+k+"-next-0.html";
    var response = UrlFetchApp.fetch(url);
    var contenttext = response.getContentText();
    var resulturl = contenttext.match(/\/news\/results\/(.*)\.html/g);
    for( var i=0 ; i < resulturl.length ; i++) {
      arr[resulturl[i]]++;
    }
  }
  
  
  var html = '<table>';
  html += '<tr bgcolor="#00F890"><th>Nos</th><th>RESULTS</th></tr>';
  var i=1;

  for(var key in arr) {
    var URL = "http://www.moneycontrol.com"+key;
    var parts = URL.split("/");
    parts = parts[parts.length - 1].split("_");
    
    if( !newarr[parts[0]] ) {
      addtocell = 1;
    
      html += '<tr bgcolor="#F0FFF0"><td>'+ i++ +'</td><td><a href="'+URL+'" style="text-decoration:none;">'+parts[0]+'</a></td></tr>';
      value += parts[0]+',';
    }
  }
  
  html += '</table>';
  if(addtocell) {
    cell.setValue(value);
    MailApp.sendEmail({
      to: "selvakumar111@gmail.com,p.yuvanesh@gmail.com",
      subject: "Result Reports of Companies",
      htmlBody: html,
    });
  }
}
