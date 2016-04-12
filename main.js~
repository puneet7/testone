  $(document).ready(function() {
  	
    function makeCounter() {                                                // This part will run ONLY once after the page loads
        var count = 0;                                                      // count will be visible to inner function.
        
        return function() {                                                 // 
            count++;                                                        // Increment count everytime a variable assigns itself to makeCounter(); 
            return count;                                                   // This can happen everytime a button is clicked
        }; 

    };
  	 
     todo_counter = makeCounter();                                          // Will be equal to inner function of makeCounter
     completed_counter = makeCounter();                                     //   

  	$("#todo_sub").click(function(e){
  		
  	 	var todoitem = document.getElementById("todo_item").value;            //Get the Task from the input text area.         
      document.getElementById("todo_item").value = "";                      //Reset the value of input text area. 
  		
      if(todoitem.trim().length == 0)                                       //Reject Blank submissions.
  			return false;                                                       

  		var i = todo_counter();                                               //Use the counter to create unique id for every 'x' in the anchor tag and every div under To-Do list.
  		
      //Create HTML for the newest task submitted and append it under To-Do List.
      var html_todo = "<div id = \"it_no"+i+"\" class = \"alert alert-danger fade in\"><span style = \"color: #E53935;\">" + todoitem + "</span><a href=\"#\" id = \"a_it_no"+i+"\" title = \"Move to completed tasks\" class=\"close\" data-dismiss=\"alert\" aria-label=\"close\">x</a></div>";
 		  $(html_todo).hide().fadeIn(300).appendTo("#todo_items");  	

      e.preventDefault();	                                                  //Prevent form submission (page refresh) to avoid resetting data.
  
  	});


  	$(document).on('click', 'a', function() {
    
      var date = new Date();                                                //Create Timestamp in 12Hr Format.
      var completed_time_stamp = " " + (date.getHours() > 12 ? (date.getHours()-12).toString() : date.getHours().toString()) + ":" + date.getMinutes().toString() + ":" + date.getSeconds().toString();

      var comp_no = completed_counter();                                    //Use the counter to create unique id's for 'x' and '&larr;' anchor tags. 
    	
      $par_div = $(this).parent("div");                                     //Get the Parent Element.
      par_div_id = $par_div.attr("id");                                     //Get the id of the Parent Element.

      var check_parent_div = par_div_id.toString().split("");               //Gets the First letter of parent id
      if(check_parent_div[0] =="c"){                                        //If first letter is c, the anchor tag clicked belongs to Completed Task and
        if(this.id.toString().split("")[0] == "r"){                         //Checks whether user wants to delete the task or 'r'-evert back to Unfinished Tasks.
            
            var rev_task = $par_div.find("span").text().split(" ");         //Split the words of reverting task in an array, Last element will be the timestamp.
            var redo_task = "";
            
            for(var i = 0; i<rev_task.length -1; i++)                       // Loop to remove
              redo_task = redo_task + rev_task[i] + " ";                    // the timesstamp when reverting back to unfinshed tasks.
            
            document.getElementById("todo_item").value = redo_task;         //Set the input task value to reverting task.
            $("#todo_sub").click();                                         //Triger the 'click submit button' event, with input text as redo_task.

        }
        
        return true;                                                        //If user doesn't want to revert the task, delete it.
      }

    	var complete = $par_div.find("span").text();                          //If the anchor tag (x) clicked belongs to To-Do List, find the text in the span tags which will be the task. 
    	var html_completed = "<div class = \"alert alert-success fade in\" id = \"c_it_no" + comp_no + "\"> <span style = \"text-decoration: line-through;\">" + complete + "</span><span class = \"tstamp\">" + completed_time_stamp + "</span><a title = \"Remove task\" href=\"#\" class=\"close\" data-dismiss=\"alert\" aria-label=\"close\">&nbsp;x</a><a id = \"rev_back\"" + comp_no + "\" title = \"Mark as unfinished\" href = \"#\" class = \"close\" data-dismiss = \"alert\">&larr;&nbsp;</a></div>";
    	$(html_completed).hide().fadeIn(300).appendTo("#completed_tasks");    //Move from To-Do List to Completed Tasks.
	
  });

});
