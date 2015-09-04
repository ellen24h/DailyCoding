### problem 
__Boiled Eggs__

__Description:__

You are the greatest chef on earth. No one boils eggs like you! Your restaurant is always full of guests, who love your boiled eggs. But when there is a greater order of boiled eggs, you need some time, because you have only one pot for your job. How much time do you need?

__Your Task__

Implement a function, which takes a non-negative integer, representing the number of eggs to boil. It must return the time in minutes (integer), which it takes to have all the eggs boiled.

__Rules__

you can put at most 8 eggs into the pot at once
it takes 5 minutes to boil an egg
we assume, that the water is boiling all the time (no time to heat up)
for simplicity we also don't consider the time it takes to put eggs into the pot or get them out of it
Example

### Examples

	cookingTime(0); // must return 0
	cookingTime(5); // must return 5
	cookingTime(10); // must return 10

### My Solution

	function cookingTime(eggs) {
	  return Math.ceil(eggs/8) * 5;
	}

### What I learned

__JavaScript parseInt() Function__

__Example__

Parse different strings:

	var a = parseInt("10") + "<br>";
	var b = parseInt("10.00") + "<br>";
	var c = parseInt("10.33") + "<br>";
	var d = parseInt("34 45 66") + "<br>";
	var e = parseInt(" 60 ") + "<br>";
	var f = parseInt("40 years") + "<br>";
	var g = parseInt("He was 40") + "<br>";

	var h = parseInt("10",10)+ "<br>";
	var i = parseInt("010")+ "<br>";
	var j = parseInt("10",8)+ "<br>";
	var k = parseInt("0x10")+ "<br>";
	var l = parseInt("10",16)+ "<br>";

	var n = a + b + c + d + e + f + g + "<br>" + h + i + j + k +l;

The result of n will be:

	10
	10
	10
	34
	60
	40
	NaN

	10
	10
	8
	16
	16


__소수점 올림, 버림, 반올림__

Math.ceil() : 소수점 올림, 정수형 반환
Math.floor() : 소수점 버림, 정수형 반환
Math.round() : 소수점 반올림, 정수형 반환

	var n = 123.456;
	alert(Math.ceil(n)); // 124
	alert(Math.round(n)); // 123

	n = 123.567;
	alert(Math.ceil(n)); // 124
	alert(Math.floor(n)); // 123
	alert(Math.round(n)); // 124 

__소수점 자리수 표기__

toFiexed() : 숫자를 문자열로 변환하면서 지정된 소수점 이하 숫자를 반올림하여 출력한다.
toExponential() : 숫자를 문자열로 변환하면서 소수점 앞의 숫자 하나와 지정된 개수의 소수점 이후 숫자로 구성되는 지수표기법을 사용하여 출력한다. 
toPrecision() : 지정된 수의 유효 숫자 개수만큼 숫자로 출력한다. 만약 유효 숫자 갯수가 숫자의 정수부분 전체를 출력할 만큼 충분하지 않으면 지수 표기법으로 출력된다. 

위 세 가지 Method는 모두 반올림하여 출력된다. 

	var n = 123.456;

	alert(n.toFixed(0)); // 123
	alert(n.toFixed(2)); // 123.46	

	alert(n.toExponential(1)); // 1.2e+2
	alert(n.toExponential(3)); // 1.235e+2

	alert(n.toPrecision(2)); // 1.2e+2
	alert(n.toPrecision(4)); // 123.5
	alert(n.toPrecision(7)); // 123.4560 


__원단위 절사__

원단위의 경우 10, 십원단위의 경우 100, 백원단위의 경우 1000, ... 을 이용하면 원단위 절사가 가능하다. 

	var n = 2117;

	n = Math.floor(n/10) * 10; // 10으로 나누면 211.7, floor 함수로 소수점을 버리면 211, 다시 10을 곱하면 2110
	alert(n); // 2110 
