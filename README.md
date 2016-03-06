# Gluttonous-Snake


window.onload = function(){
	console.log(1);
	var arr = [[0,0],[0,1],[0,2]];
		UP = 38 ; 
		DOWN = 40 ;
		LEFT = 37 ;
		RIGHT = 39 ;
	$(arr[2][0] + '-' + arr[2][1]).style.backgroundColor = 'purple';
	huashe();		
	var direction = RIGHT ;
	function $(id){
		return document.getElementById(id);
	}
	function join(arr){
		return arr[0] + '-' + arr[1];
	}
	function huashe(){
		for ( var i = 0; i < arr.length-1; i++ ){
			var el = arr[i][0] + '-' +arr[i][1];
			$(el).style.backgroundColor = 'red';
		}
	}
	function panduan(x,y){
		for(var i = 0 ; i < arr.length ; i++){
			if( x == arr[i][0] && y == arr[i][1]){
				return true;
			}
		}
		return false;
	}
	function toufangshiwu(){
		x = Math.floor(Math.random()*10);
		y = Math.floor(Math.random()*10);
		while(panduan(x,y)){
			x = Math.floor(Math.random()*10);
			y = Math.floor(Math.random()*10);
		}
		$(join([x,y])).style.backgroundColor = 'green';
		return [x,y];
	}
	var shiwu = toufangshiwu();
	var timeId = setInterval(function(){
		var oldHead = arr[arr.length-1],newHead;
		if( direction == RIGHT) newHead = [ oldHead[0] , oldHead[1]+1 ];
		if( direction == LEFT) newHead = [ oldHead[0] , oldHead[1]-1 ];
		if( direction == UP) newHead = [ oldHead[0]-1 , oldHead[1] ];
		if( direction == DOWN) newHead = [ oldHead[0]+1 , oldHead[1] ];
		if( newHead[1] < 0 ){
			newHead[1] = 9;
		}
		if( newHead[1] > 9 ){
			newHead[1] = 0;
		}
		if( newHead[0] > 9){
			newHead[0] = 0;
		}
		if( newHead[0] < 0){
			newHead[0] = 9;
		}
		// if( newHead[1] > 9 || newHead[1] < 0 || newHead[0] > 9 || newHead[0] < 0){
		// 	alert('Game over');
		// 	clearInterval(timeId);
		// 	return;
		// } 
		if( newHead[0] == x && newHead[1] == y ){
			arr.push(shiwu);
			$(join([x,y])).style.backgroundColor = 'purple';
			$( join(arr[arr.length-2]) ).style.backgroundColor = 'red';
			shiwu = toufangshiwu();
			return;
		}
		for ( var i = 0 ; i < arr.length ; i++ ){
			if( newHead[0] == arr[i][0] && newHead[1] == arr[i][1]){
				alert('Game over');
				clearInterval(timeId);
				return;
			}
		}
		if( arr.length == 100){
			alert('恭喜，您已完成通关！！！')
		}
		arr.push(newHead);
		$( join(newHead) ).style.backgroundColor = 'purple';
		$( join(arr[arr.length-2]) ).style.backgroundColor = 'red';
		var tail = arr.shift();
		$(join(tail)).style.backgroundColor = 'white';
	},300);
	document.onkeydown = function(ev){
		console.log(ev.keyCode);
		var tmp = Math.abs(ev.keyCode - direction) ;
		if( tmp == 2){
			return false;
		}
		if( ev.keyCode != RIGHT && ev.keyCode != LEFT && ev.keyCode != DOWN && ev.keyCode != UP ){
			return;
		}
		direction = ev.keyCode ;
	}
}
