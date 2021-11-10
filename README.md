
<!DOCTYPE html>

<html lang="en" xmlns="http://www.w3.org/1999/xhtml">
<head>
    <meta charset="utf-8" />
    <title>Aplikasi kalkulator</title>
    <link rel="stylesheet" type="text/css" href="style.css">
    <h1 style="color:green;"><marquee>Kalkulator Uchiha Al Nolimit alias Ahmad Saefudin Al Bayani</marquee></h1><hr style="color:green;">
  
  
</head>
<body>
    <style>
    body{
    box-sizing: border-box;
    width: 100%;
    height: 100%;
    overflow-x: hidden;
    background-image:url(2.jpeg);

}


button {
    height: 50px;
    margin: 2px;
    font-size: 1.2em;
    border-style: none;
    background-color: lime;
}


button:hover {
    color: red;
    background-color: #4b0082;
    cursor: pointer;
    border: 2px solid white;
}

.calculator {
    position: relative;
    top: 90px;
    margin: 0 auto;
    max-width: 300px;

   
}

.calcButtons {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr;
    margin:0 auto;
    background-color: #000000;
    padding: 10px;
}

.calcButtons > button:nth-child(17) {
 
    grid-column: 1/3;
}

.operator {
    background-color: #d6e0f5;
}

.number {
    background-color: #adff2f;
}

.userInput {
    position: relative;
    height: 80px;
    max-width: 100%;
    text-align: right;
    padding: 10px;
    font-size: 25px;
    border: 1px solid #193366;
    background-color: #d6e0f5;
}



.calcButtons > button:nth-child(19) {

    background-color: grey;
}

.userEntry {
    position: absolute;
    bottom: 0;
    padding: 0;
    margin: 5px;
    right:0;
}

.finalCalc{

    position: absolute;
    right:0;
    margin:5px;
    top:0;
    padding:0;
}

    </style>


<div class="calculator">

    <div class="userInput"><p class="userEntry"></p><p class="finalCalc"></p></div>

    <div class="calcButtons">
    

        <button>+/-</button>
        <button>AC</button>
        <button>DEL</button>
        <button class="operator">*</button>

        <button class="number">1</button>
        <button class="number">2</button>
        <button class="number">3</button>
        <button class="operator">+</button>

        <button class="number">4</button>
        <button class="number">5</button>
        <button class="number">6</button>
        <button class="operator">/</button>
    
        <button class="number">7</button>
        <button class="number">8</button>
        <button class="number">9</button>
        <button class="operator">-</button>

    
        <button class="number">0</button>
        <button class="decimal">.</button>
        <button class="operator">=</button>


    </div>
</div>

<script src="script.js"></script>
    <script>
    let $buttons = document.querySelectorAll("button");
let ui = document.querySelector(".userEntry");
let finalCalc = document.querySelector(".finalCalc");
let opPressed = false;

let valOne = [];
let valTwo = [];
var operator = [];
let finalAnswer = 0;


[...$buttons].map(x => {
    x.addEventListener("click", function (e) {

        switch (this.innerHTML) {
            case "AC":
                clearDisplay();
                break;
            case "DEL":
                removeNumber();
                break;
            case "+/-":
                makeNegative();
                break;
            case "=":
                makeCalculation();
                break;    
            case "+":
                operator.splice(0, 1, this.innerHTML)
                console.log(operator);

                storeValue();
                break;
            case "*":
                operator.splice(0, 1, this.innerHTML)
                console.log(operator);

                storeValue();
                break;
            case "/":
                operator.splice(0, 1, this.innerHTML)
                console.log(operator);

                storeValue();
                break;
            case "-":
                operator.splice(0, 1, this.innerHTML);
                console.log(operator);
                storeValue();
                break;
            default:
                 if (valOne.length >11) {
                    alert("Tidak Ada Nilai Lagi Diluar 8");
                }

                 else {

                    valOne.push(this.innerText);
                    ui.textContent = valOne.join("");
                    console.log(valOne);

                }
                break;
            case ".":
                if (valOne.includes(".")) {
                    alert("Anda Tidak Dapat Menggunakan Decimal Lagi");
                } else {
                    valOne.push(this.innerText);
                    ui.textContent = valOne.join("");

                }
                break;

        }

    })
})



//function add(a, b) {

//    return a + b;
//}


//function subtract(a, b) {
//    return a - b;
//}

//function divide(a, b){

//    return a / b;
//}

//function multiply(a, b){

//    return a * b;
//}

//function module(a, b) {

//    return a % b;
//}



function clearDisplay() {

    ui.textContent = "";
    finalCalc.textContent = ""
    valOne = [];
    valTwo = [];
    operator = [];
}

function removeNumber(e) {

    valOne.pop();
    ui.textContent = valOne.join("");
}


function makeNegative() {

    if (valOne.length < 1) {
        return false;
    }else if(valOne[0] == "-") {
        valOne.shift()

    } else {
        valOne.unshift("-")

    }
    ui.textContent = valOne.join("");
}

function makeCalculation() {

    if (valTwo.length > 0 && operator.length!==0) {
        //finalAnswer = valTwo.concat(operator, valOne).join("");
        finalAnswer = eval(valTwo + operator + valOne.join(""));
        finalCalc.textContent = "";
        finalCalc.textContent = eval(finalAnswer).toFixed(2);
        ui.textContent = "";
        valTwo = eval(finalAnswer);
        valOne = [];
        //operator = [];

    } else if (operator.length == 0) {

        alert("Perhitungan Tidak Valid, Tidak Ada Operator");
        
    }

    else {
        //finalAnswer = valTwo.concat(operator, valOne).join
        finalAnswer = finalAnswer = eval(valTwo + operator + valOne.join(""));

        console.log("final answer");
        console.log(finalAnswer);
        finalCalc.textContent = "";
        ui.textContent = "";
        finalCalc.textContent = eval(finalAnswer).toFixed(2);
        //operator = [];
        valTwo = eval(finalAnswer);
        valOne = [];



    }


 

    
}

function storeValue() {




        if (valOne.length == 0 && valTwo.length==0) {
            return false;
        } else if (valTwo.length > 0) {
            finalCalc.textContent = valTwo + " " + operator;
          

            
        }else if(valTwo.length==0) {
            valTwo.push(valOne.join(""));
            valOne = [];
            ui.textContent = "";
            finalCalc.textContent = "";
            finalCalc.textContent = valTwo + " " + operator

            
    }
        finalCalc.textContent = valTwo + " " + operator;

       
        
}
    </script>

</body>
</html>
