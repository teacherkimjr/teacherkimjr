<!DOCTYPE html>
<html>
<body>

<p><textarea id="targetText" style="width:300px;height:200px"></textarea></p>
<p><button onclick="sliceText()">Check Text</button></p>
<p id="result"></p>

<script>
function sliceText(){
	var targetText = document.getElementById("targetText").value;
	var sliceWord = "";
	var result = {};
	var indexOfSlice = getIndexOfSlice(targetText);
	
	while(indexOfSlice != -1){
		sliceWord = targetText.slice(0, indexOfSlice);
		targetText = targetText.slice(indexOfSlice + 1);
		
		if(sliceWord != ""){
			if(result[sliceWord] == null){
				result[sliceWord] = 1;
			}else{
				result[sliceWord] += 1;
			}
		}
		indexOfSlice = getIndexOfSlice(targetText);
	}
	if(targetText != ""){
		if(result[targetText] == null){
			result[targetText] = 1;
		}else{
			result[targetText] += 1;
		}
	}
	
	var resultString = "";
	for(i in result){
		resultString = resultString + i + " : " + result[i] + "<br>";
	}
	
	document.getElementById("result").innerHTML = resultString;
}

function getIndexOfSlice(targetText){
	var indexOfBlank = targetText.indexOf(" ");
	var indexOfNewline = targetText.indexOf("\n");
	if(indexOfBlank != -1 && indexOfNewline == -1){
		return indexOfBlank;
	}
	if(indexOfBlank == -1 && indexOfNewline != -1){
		return indexOfNewline;
	}
	if(indexOfBlank < indexOfNewline){
		return indexOfBlank;
	}else{
		return indexOfNewline;
	}
}
</script>
</body>
</html>
