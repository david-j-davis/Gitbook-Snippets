# JS Snippets

####AJAX Example
---

    $(document).ready(function () {

     $('form').submit(function(e) {
          e.preventDafault();
          var url = $(this).attr("action");
          //Grab data
          var formData = $(this).serialize();
          //Post data
          $.ajax(url, {
               data: formData,
               type: "POST",
               success: function(response) {
                    $(#some-div).html('<p>Thanks for signing up</p>');
               };

          }).fail(function (jqXHR) {
               $('#myDiv').html("<p>Sorry! " + jqXHR.statusText + "error.</p>");
          }); //End ajax

     }); //End submit function 
     }); //End DOM ready



