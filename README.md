# validationLibrary
function validation(x) {
	x.validate = function(y){
		var err = [];
		for(i=0; i<y.length; i++){

			if(y[i].type == "required"){
				if (x.value.trim()==""){
					err.push("cannot be empty");
				}
			}

			if(y[i].type == "text"){
				if (!isNaN(x.value)) {
					err.push("Cannot be a Number");
				}
			}

			if(y[i].type == "regex") {
				var reg = y[i].pattern;
				if(!x.value.match(reg)){
					err.push("invalid format");
				}
			}

			if(y[i].type == "length"){
				if((x.value.length) < 8){
					err.push("its too short, minimum 8 characters");
				}
			
				if((x.value.length) > 42){
					err.push("its too long, maximum 42 characters");
				}

				if((x.value.length) != 10){
					err.push("10 characters reequired");
				}
			}

			if(y[i].type == "time"){
				var timeVal = x.value;
					if (!timeVal.match(/^\d{1,2}:\d{2}([ap]m)?$/))
   					err.push("invalid format, required ex. (10:20 pm)");
			}

			if(y[i].type == "date"){
				if (!dateVal.match(/^\d{1,2}\/\d{1,2}\/\d{4}$/))
					   err.push("invalid date format");
					   
				else {
					var currDate = new Date();
					var date = currDate.getDate();
					var month = currDate.getMonth();
					var year = currDate.getFullYear();
					var monthDayArray = [31,31,28,31,30,31,30,31,31,30,31,30];

					var enterdate = x.value.split("/");

					 if(enterdate[2] == year){

						if(enterdate[1] == month){
								if(abs(enterdate[0]-date) < 3)
								err.push("date entered should be atleast 3 business days from now");
						}	

						else if(enterdate[1]-month == 1){
							if(monthDayArray[month%12] - date + enterdate[0] < 3){
								err.push("date entered should be atleast 3 business days from now");
							}
						}
						
						else if(enterdate[1] < month)
						err.push("date entered should be atleast 3 business days from now");

						else;
					 }

					 else if(enterdate[2] - year == 1){
							if(!(enterdate[1] == 1 && month == 12))
							err.push("date entered should be atleast 3 business days from now");	
							
							else {
								if(31 - date + enterdate[0] < 3)
								err.push("date entered should be atleast 3 business days from now");
							}
					 }
					
					 else if(enterdate[2] < year)
						err.push("date entered should be atleast 3 business days from now");
						

					 else;
				}
			}

			if(y[i].type == "file"){
					var filePath = x.value;
					var allowedExtensions = /(\.jpg|\.jpeg|\.png|\.gif)$/i;
					if(!allowedExtensions.exec(filePath)){
						err.push("Please upload file having extensions .jpeg/.jpg/.png/.gif only.");
					}
			}

			

			if(y[i].type == "email"){
				var mailformat = /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/;
				if(!x.value.match(mailformat))
				{
					err.push("You have entered an invalid email address!");
				}
				
			}
		}
	if(err==[]){
		return true;
	}
	else {
		return err;
	}

	}
	return(x);
}

j = document.getElementById('first');
console.log(j);
validation(j).validate([{type:"required"}, {type: "text"}]);
console.log(typeof(j.value));

