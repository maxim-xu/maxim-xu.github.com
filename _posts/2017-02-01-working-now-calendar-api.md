---
layout: post
title: Working Now Tutors via Google Calendar
tags: cissandbox
categories: developer
date:   2017-01-30 15:05:14 -0500
comments: true
--- 
 
<html>
  <head>
    <title>Working Now Tutors</title>
      <meta charset='utf-8' />
      <script
              src="https://code.jquery.com/jquery-2.2.4.min.js"
              integrity="sha256-BbhdlvQf/xTY9gja0Dq3HiwQF8LaCRTXxZKRutelT44="
              crossorigin="anonymous"></script>
      <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery-timepicker/1.10.0/jquery.timepicker.min.js"></script>
      <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/jquery-timepicker/1.10.0/jquery.timepicker.min.css" />
      <script src="https://cdnjs.cloudflare.com/ajax/libs/bootstrap-datepicker/1.6.4/js/bootstrap-datepicker.min.js"></script>
      <link rel="stylesheet" type="text/css" href="https://cdnjs.cloudflare.com/ajax/libs/bootstrap-datepicker/1.5.0/css/bootstrap-datepicker.standalone.css">

      <link rel="stylesheet" href="https://ajax.googleapis.com/ajax/libs/jqueryui/1.7.2/themes/ui-lightness/jquery-ui.css" type="text/css" media="all">
      <script src="http://jonthornton.github.io/Datepair.js/dist/datepair.js"></script>
      <script src="http://jonthornton.github.io/Datepair.js/dist/jquery.datepair.js"></script>

      <style>
          body {
              height:100%;
          }
          .tutors {
              display: inline-block;
              margin-right: 30px;
          }
          #title {
              margin-bottom: 0;
          }
          #onSelect {
              margin-bottom: .75rem;
          }
          #apply {
              padding:5px;
              background-color: #fff;
              border: 1px solid #ddd;
              font-family: inherit;
              cursor: pointer;
              margin-left: 4px;
          }
      </style>
  </head>
   <body>
   <p id="title"><b>Select a time today:</b></p>
    <p id="onSelect">
        <select id="onSelectTime" type="text" class="time start" />
        <button id="apply">Apply Time</button>
    </p>
    <br />
    <p id="tutors"></p>

    <script type="text/javascript">
        var baseURL = "https://www.googleapis.com/calendar/v3/calendars/bentleycis@gmail.com/events?&timeMin=";
        var APIKey = "&key=AIzaSyCN8NNyQEJAeXf58TsoL2RdYj6Qn0EsmB0";
        var currentTime = ISODateString(new Date());
        var midnight = new Date();
        midnight.setHours(34,0,0,0);
        var timeMax = ISODateString(midnight);
        var todayEvents = [];
        var imageBaseURL = "http://cis.bentley.edu/sandbox/wp-content/uploads/TutorImage/";
        var imageSize = "-150x150.jpg";

        function init() {
        $.getJSON(baseURL + currentTime + "&timeMax=" + timeMax + APIKey, function(data){
            $.extend(todayEvents, data.items);
        }).done(function() {
            for (i=0;i<todayEvents.length;i++) {
                if (todayEvents[i].summary.includes("Emily")) {
                    todayEvents[i].summary = "Emilyk"
                }
                if (currentTime >= todayEvents[i].start.dateTime && currentTime <= todayEvents[i].end.dateTime) {
 
                    $('#tutors').append('<div class="tutors"><p>' + todayEvents[i].summary + '</p>' + '<img src="' + imageBaseURL + todayEvents[i].summary.toLowerCase() + imageSize + '"/></div>');

                        }
                    }
            }
            );
        }

        // convert date to RFC3339 timestamp
        function pad(n) {
            return n<10 ? '0'+n : n
        }

        function ISODateString(d) {
            return d.getUTCFullYear()+'-'
                + pad(d.getUTCMonth()+1)+'-'
                + pad(d.getUTCDate())+'T'
                + pad(d.getUTCHours()-5)+':'
                + pad(d.getUTCMinutes())+':'
                + pad(d.getUTCSeconds())+'Z'
        }

        function convertPickerTime(d) {
            return d.getUTCFullYear()+'-'
                + pad(d.getUTCMonth()+1)+'-'
                + pad(d.getUTCDate())+'T'
                + pad(d.getUTCHours()-5)+':'
                + pad(d.getUTCMinutes())+':'
                + pad(d.getUTCSeconds())+'Z'
        }

        init();


        $('#onSelect .time').timepicker({
            'showDuration': false,
            'timeFormat': 'H:i',
            'minTime': '10:00',
            'maxTime': '23:00'
        });


        $('#onSelect').datepair(); 

        $('#apply').click(function() {
            if ($('#onSelectTime').val() !== "") {
                var now = (new Date()).toISOString().slice(0,10);
                var $time = $('#onSelectTime').val() + ":00Z";
                currentTime = now + "T" + $time;
                $('.tutors').remove();
                init();
            }
        });

       </script>
  </body>
</html>