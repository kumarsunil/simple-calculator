<HEAD>
    <TITLE> Simple Calculation</TITLE>
    <style>
        input[type="button"]{
            background-color: beige;
            width: 35px;
            line-height: 20px;
            padding: 3px;
            margin: 0 auto;
            margin-top: 5px;
        }
        input[type="button"]:hover{
            background-color: lightblue;
        }
        #screen{
            width:99%;
            background-color: lavender;
            height: 30px;
            font-size: 12px;
            font-weight: bold;
            overflow: scroll;
        }
    </style>

</HEAD>

<BODY style="margin: 0 auto;width: 165px;height: 185px;">
<FORM NAME="myForm">
    <TABLE BORDER=2>
        <TR>
            <TD align="center">
                <INPUT TYPE="text" ID="screen" NAME="screen"><br>
            </TD>
        </TR>
        <TR>
            <TD>
                <INPUT TYPE="button" NAME="7" VALUE="  7  " onclick="update(7)">
                <INPUT TYPE="button" NAME="8" VALUE="  8  " onclick="update(8)">
                <INPUT TYPE="button" NAME="9" VALUE="  9  " onclick="update(9)">
                <INPUT TYPE="button" NAME="+" VALUE="  +  " onclick="update('+')">
                <br>
                <INPUT TYPE="button" NAME="4" VALUE="  4  " onclick="update(4)">
                <INPUT TYPE="button" NAME="5" VALUE="  5  " onclick="update(5)">
                <INPUT TYPE="button" NAME="6" VALUE="  6  " onclick="update(6)">
                <INPUT TYPE="button" NAME="-" VALUE="  -  " onclick="update('-')">
                <br>
                <INPUT TYPE="button" NAME="1" VALUE="  1  " onclick="update(1)">
                <INPUT TYPE="button" NAME="2" VALUE="  2  " onclick="update(2)">
                <INPUT TYPE="button" NAME="3" VALUE="  3  " onclick="update(3)">
                <INPUT TYPE="button" NAME="*" VALUE="  x  " onclick="update('*')">
                <br>
                <INPUT TYPE="button" NAME="c" VALUE="  c  " onclick="reset();">
                <INPUT TYPE="button" NAME="0" VALUE="  0  " onclick="update(0)">
                <INPUT TYPE="button" NAME="=" VALUE="  =  " onclick="result();">
                <INPUT TYPE="button" NAME="/" VALUE="  /  " onclick="update('/')">
            </TD>
        </TR>
    </TABLE>
</FORM>
<script type="text/javascript">
    function update(value) {
        var cVal = document.getElementById("screen").value;
        document.getElementById("screen").value = cVal + value;

    }

    function result() {
        var input = document.getElementById("screen").value;
        var values = [];
        var oprators = [];
        var left = true;
        var start = 0;
        var input2 = input;
        for (var x = 0; x < input.length; x++){
            if(input[x] == '+' || input[x] == '-' || input[x] == '*' || input[x] == '/'){
                var val = input2.slice(start, input2.indexOf(input[x]));
                values.push(val);
                oprators.push(input[x]);
                input2 = input2.substr(input2.indexOf(input[x]) + 1);
            }else if(/^\d+$/.test(input2)){
                values.push(input2);
                input = "";
            }
        }
        oprators.forEach(function(item){
            switch(item){
                case '+':
                    values.unshift(addValue(values.shift(), values.shift()));
                    break;
                case '-':
                    values.unshift(subValue(values.shift(), values.shift()));
                    break;
                case '*':
                    values.unshift(mulValue(values.shift(), values.shift()));
                    break;
                case '/':
                    values.unshift(devideValue(values.shift(), values.shift()));
                    break;
            }
        });
        document.getElementById("screen").value = values[0];
        return values[0];
    }

    function reset() {
        document.getElementById("screen").value = '';
    }

    function addValue(a,b){
        return (parseInt(a) + parseInt(b));
    }
    function subValue(a,b){
        return (parseInt(a) - parseInt(b));
    }
    function mulValue(a,b){
        return (parseInt(a) * parseInt(b));
    }
    function devideValue(a,b){
        return (parseInt(a) / parseInt(b));
    }


</SCRIPT>
</BODY>

</HTML>
