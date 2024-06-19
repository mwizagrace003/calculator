NAME: ISHIMWE MWIZA grace 
ID: 25192

                               CALCULATOR


This Flutter code creates a simple calculator application with a graphical user interface. 

1. Import Flutter Package
-> import 'package:flutter/material.dart';
* This line imports the Flutter material package, which provides the necessary widgets and classes to build a material design application.
  
2. Main Function
-> void main() {
  runApp(SimpleCalculator());
}
* The main function is the entry point of the Flutter application. It calls the runApp function with the SimpleCalculator widget as its argument, which initializes the app and starts the rendering process.

  
3. SimpleCalculator Class
-> class SimpleCalculator extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
        title: 'Calculator',
        home: Calculation(),
        theme: ThemeData.dark()
    );
  }
}
* Class Definition: SimpleCalculator extends StatelessWidget, indicating that this widget does not maintain any state.
build Method: The build method returns a MaterialApp widget that sets the app title to 'Calculator', uses the Calculation widget as the home screen, and applies a dark theme.


4. Calculation Class
-> class Calculation extends StatefulWidget{
  @override
  _CalculationState createState() => _CalculationState();
}
* Class Definition: Calculation extends StatefulWidget, indicating that this widget maintains state.
createState Method: Creates an instance of the _CalculationState class, which holds the state of the Calculation widget.


5. CalculationState Class
-> class _CalculationState extends State<Calculation> {
  List<dynamic> inputList = [0];
  String output = '0';

* State Variables:
inputList: A list that stores the sequence of numbers and operators input by the user.
output: A string that stores the current output to be displayed on the screen.

6. Handling Clear Operation
-> void _handleClear() {
  setState(() {
    inputList = [0];
    output = '0';
  });
}
* This method clears the input list and resets the output to '0'. It uses setState to notify the framework that the state has changed and the UI needs to be updated.

7. Handling Button Press
-> void _handlePress(String input) {
  setState(() {
    if (_isOperator(input)) {
      if (inputList.last is int) {
        inputList.add(input);
        output += input;
      }
    } else if (input == '=') {
      while (inputList.length > 2) {
        int firstNumber = inputList.removeAt(0) as int;
        String operator = inputList.removeAt(0);
        int secondNumber = inputList.removeAt(0) as int;
        int partialResult = 0;

        if (operator == '+') {
          partialResult = firstNumber + secondNumber;
        } else if (operator == '-') {
          partialResult = firstNumber - secondNumber;
        } else if (operator == '*') {
          partialResult = firstNumber * secondNumber;
        } else if (operator == '/') {
          partialResult = firstNumber ~/ secondNumber;
          if(secondNumber == 0) {
            partialResult = firstNumber;
          }
        }

        inputList.insert(0, partialResult);
      }

      output = '${inputList[0]}';
    } else {
      int? inputNumber = int.tryParse(input);
      if (inputNumber != null) {
        if (inputList.last is int && !_isOperator(output[output.length - 1])) {
          int lastNumber = (inputList.last as int);
          lastNumber = lastNumber * 10 + inputNumber;
          inputList.last = lastNumber;

          output = output.substring(0, output.length - 1) + lastNumber.toString();
        } else {
          inputList.add(inputNumber);
          output += input;
        }
      }
    }
  });
}
* Operators: If the input is an operator (+, -, *, /), it is added to the inputList if the last element is a number.
Equals: When the equals (=) button is pressed, the list is processed in a loop to perform the calculations step-by-step and update the output with the final result.
Numbers: If the input is a number, it either appends to the last number in the list (if the last input was also a number) or adds a new number to the list.


8. Utility Method
-> bool _isOperator(String input) {
  if (input == "+" || input == "-" || input == "*" || input == "/") {
    return true;
  }
  return false;
}
* This method checks if the input string is an operator.
