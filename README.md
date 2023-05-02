Download Link: https://assignmentchef.com/product/solved-cpe202-project-2-evaluating-expressions-using-stacks
<br>
For this project, you will implement a program to evaluate a <u><a href="https://en.wikipedia.org/wiki/Reverse_Polish_notation">postfix (Reverse Polish or RPN) expression</a></u><a href="https://en.wikipedia.org/wiki/Reverse_Polish_notation">.</a> To make the program more versatile, you’ll also provide code to convert infix expressions (the kind used in standard arithmetic) and <u><a href="https://en.wikipedia.org/wiki/Polish_notation">prefix (Polish or PN) expressions</a></u> to postfix expressions.  In this way, your program will be able to evaluate prefix, infix and postfix expressions. Many language translators (e.g. compiler) do something similar to convert expressions into code that is easy to execute on a computer.

For this assignment, you will use an implementation of the Abstract Data Type Stack. Your programs should work with either implementation from Lab 2 – the one based on a linked data structure or the one based on Python’s List data type, but for consistency with grading, use the <strong>stack_array.py</strong> implementation.  You must <strong>add, commit, and push</strong> a correct implementation of this file.

<strong>Notes</strong>:

<ul>

 <li>Postfix expressions will only consist of numbers (<u>integers, reals, positive or negative</u>) and the five operators separated by spaces. You may assume a capacity of 30 for the Stack will be sufficient for any expression that your programs will be required to handle.</li>

 <li>In addition to the operators + – * / shown in class, your programs should handle the exponentiation operator. In this assignment, the exponential operator will be denoted by ^.  For example, 2^38 and</li>

</ul>

3^29.  (https://en.wikipedia.org/wiki/Exponentiation)

<ul>

 <li>For infix expressions, the exponentiation operator has higher precedence than the * or /. For example, 2*3^2 = 2*9 = 18 not 6^2=36</li>

 <li>Also, for infix expressions, the exponentiation operator associates from right to left. The other operators (+,-,*,/) associate left to right. Think carefully about what this means.  For example: 2^3^2 = 2^(3^2) = 2^9 = 512 not (2^3)^2= 8^2=64</li>

 <li>Infix expressions may also have parentheses – consider that for the infix_to_postfix() function.</li>

 <li>Every class and function must come with a brief purpose statement in its docstring. In separate comments you should explain the arguments and what is returned by the function or method.</li>

 <li>You must provide test cases that completely test all functions.</li>

 <li>Use descriptive names for data structures and helper functions. You must name your files and functions (methods) as specified in the starter code provided to you.</li>

</ul>

<h1>2. Modules and Functions</h1>

Your code will be contained in these files:

<ul>

 <li>py</li>

 <li>py</li>

 <li>py</li>

</ul>







<h1>3. Algorithms</h1>




<h2>Evaluating a Postfix (RPN) Expression</h2>




While RPN will look strange until you are familiar with it, here you can begin to see some of its advantages for programmers. One such advantage of RPN is that it removes the need for parentheses. Infix notation supports operator precedence ( and ∕ have higher precedence than + and −) and thus needs parentheses to override this precedence. This makes parsing such expressions much more difficult. RPN has no notion of precedence, the operators are processed in the order they are encountered. This makes evaluating RPN expressions fairly straightforward and is a perfect application for a stack data structure, just follow these steps:




<ul>

 <li>Process the expression from left-to-right When a value is encountered: o Push the value onto the stack</li>

 <li>When an operator is encountered:

  <ul>

   <li>Pop the required number of values from the stack o Perform the operation</li>

   <li>Push the result back onto the stack</li>

  </ul></li>

 <li>Return the last value remaining on the stack For example, given the expression <strong>5 1 2 + 4 ^ + 3 –</strong> :</li>

</ul>




<table width="0">

 <tbody>

  <tr>

   <td width="58"><strong>Input </strong></td>

   <td width="77"><strong>Type </strong></td>

   <td width="58"><strong>Stack </strong></td>

   <td width="526"><strong>Notes </strong></td>

  </tr>

  <tr>

   <td width="58">5</td>

   <td width="77">Value</td>

   <td width="58">5</td>

   <td width="526">Push 5 onto stack</td>

  </tr>

  <tr>

   <td width="58">1</td>

   <td width="77">Value</td>

   <td width="58">1 5</td>

   <td width="526">Push 1 onto stack</td>

  </tr>

  <tr>

   <td width="58">2</td>

   <td width="77">Value</td>

   <td width="58">2 1 5</td>

   <td width="526">Push 2 onto stack</td>

  </tr>

  <tr>

   <td width="58">+</td>

   <td width="77">Operator</td>

   <td width="58">3 5</td>

   <td width="526">Pop two operands (1, 2), perform operation (1+2=31+2=3), and push result onto stack</td>

  </tr>

  <tr>

   <td width="58">4</td>

   <td width="77">Value</td>

   <td width="58">4 3 5</td>

   <td width="526">Push 4 onto stack</td>

  </tr>

  <tr>

   <td width="58">^</td>

   <td width="77">Operator</td>

   <td width="58">81 5</td>

   <td width="526">Pop two operands (3, 4), perform operation (34=8134=81), and push result onto stack</td>

  </tr>

  <tr>

   <td width="58">+</td>

   <td width="77">Operator</td>

   <td width="58">86</td>

   <td width="526">Pop two operands (5, 81), perform operation (5+81=865+81=86), and push result onto stack</td>

  </tr>

  <tr>

   <td width="58">3</td>

   <td width="77">Value</td>

   <td width="58">3 86</td>

   <td width="526">Push 3 onto stack</td>

  </tr>

  <tr>

   <td width="58">−</td>

   <td width="77">Operator</td>

   <td width="58">83</td>

   <td width="526">Pop two operands (86, 3), perform operator (86−3=1486−3=14), and push result onto stack</td>

  </tr>

  <tr>

   <td width="58"></td>

   <td width="77">Result</td>

   <td width="58">83</td>

   <td width="526"></td>

  </tr>

 </tbody>

</table>










<h2>Converting Infix Expressions to Postfix (RPN)</h2>




You can also use a stack to convert an infix expression to an RPN expression via the <u><a href="https://en.wikipedia.org/wiki/Shunting-yard_algorithm">Shunting</a><a href="https://en.wikipedia.org/wiki/Shunting-yard_algorithm">–</a><a href="https://en.wikipedia.org/wiki/Shunting-yard_algorithm">yard algorithm</a></u><a href="https://en.wikipedia.org/wiki/Shunting-yard_algorithm">.</a> The steps are shown below. Note that the algorithm is more complex that what was shown in class, because the project will include a power operator.

<ul>

 <li>Process the expression from left-to-right When you encounter a value:

  <ul>

   <li>Append the value to the RPN expression</li>

  </ul></li>

 <li>When you encounter an opening parenthesis: o Push it onto the stack</li>

 <li>When you encounter a closing parenthesis: o Until the top of stack is an opening parenthesis, pop operators off the stack and append them to the RPN expression

  <ul>

   <li>Pop the opening parenthesis from the stack (but don’t put it into the RPN expression)</li>

  </ul></li>

 <li>When you encounter an operator, o<sub>1</sub>: o While there is an operator, o<sub>2</sub>, at the top of the stack and either</li>

</ul>

o<sub>1</sub>is left-associative and its precedence is <em>less than or equal to</em> that of o<sub>2</sub>, or o<sub>1</sub> is right-associative, and has precedence <em>less than</em> that of o<sub>2</sub>

&#x25aa;   Pop o<sub>2</sub> from the stack and append it to the RPN expression o          Finally, push o<sub>1</sub> onto the stack

<ul>

 <li>When you get to the end of the infix expression, pop (and append to the RPN expression) all remaining operators</li>

</ul>

For example, given the expression <strong>3 + 4 * 2 / ( 1 – 5 ) ^ 2 ^ 3</strong>:




<table width="0">

 <tbody>

  <tr>

   <td width="80"><strong>operator </strong></td>

   <td width="96"><strong>precedence </strong></td>

   <td width="104"><strong>associativity </strong></td>

  </tr>

  <tr>

   <td width="80">^</td>

   <td width="96">high</td>

   <td width="104">Right</td>

  </tr>

  <tr>

   <td width="80">*</td>

   <td width="96">medium</td>

   <td width="104">Left</td>

  </tr>

  <tr>

   <td width="80">/</td>

   <td width="96">medium</td>

   <td width="104">Left</td>

  </tr>

  <tr>

   <td width="80">+</td>

   <td width="96">low</td>

   <td width="104">Left</td>

  </tr>

  <tr>

   <td width="80">−</td>

   <td width="96">low</td>

   <td width="104">Left</td>

  </tr>

 </tbody>

</table>




<table width="0">

 <tbody>

  <tr>

   <td width="58"><strong>Input </strong></td>

   <td width="162"><strong>Action </strong></td>

   <td width="141"><strong>RPN </strong></td>

   <td width="60"><strong>Stack </strong></td>

   <td width="298"><strong>Notes </strong></td>

  </tr>

  <tr>

   <td width="58">3</td>

   <td width="162">Append 3 to expression</td>

   <td width="141">3</td>

   <td width="60"></td>

   <td width="298"></td>

  </tr>

  <tr>

   <td width="58">+</td>

   <td width="162">Push + onto stack</td>

   <td width="141">3</td>

   <td width="60">+</td>

   <td width="298"></td>

  </tr>

  <tr>

   <td width="58">4</td>

   <td width="162">Append 4 to expression</td>

   <td width="141">3 4</td>

   <td width="60">+</td>

   <td width="298"></td>

  </tr>

  <tr>

   <td width="58">*</td>

   <td width="162">Push * onto stack</td>

   <td width="141">3 4</td>

   <td width="60">* +</td>

   <td width="298">* has higher precedence than +</td>

  </tr>

  <tr>

   <td width="58">2</td>

   <td width="162">Append 2 to expression</td>

   <td width="141">3 4 2</td>

   <td width="60">* +</td>

   <td width="298"></td>

  </tr>

  <tr>

   <td width="58">/</td>

   <td width="162">Pop *, push /</td>

   <td width="141">3 4 2 *</td>

   <td width="60">/ +</td>

   <td width="298">/ and * have same precedence/ has higher precedence than +</td>

  </tr>

  <tr>

   <td width="58">(</td>

   <td width="162">Push ( to stack</td>

   <td width="141">3 4 2 *</td>

   <td width="60">( / +</td>

   <td width="298"></td>

  </tr>

  <tr>

   <td width="58">1</td>

   <td width="162">Append 1 to expression</td>

   <td width="141">3 4 2 * 1</td>

   <td width="60">( / +</td>

   <td width="298"></td>

  </tr>

  <tr>

   <td width="58">–</td>

   <td width="162">Push – to stack</td>

   <td width="141">3 4 2 * 1</td>

   <td width="60">– ( / +</td>

   <td width="298"></td>

  </tr>

  <tr>

   <td width="58">5</td>

   <td width="162">Append 5 to expression</td>

   <td width="141">3 4 2 * 1 5</td>

   <td width="60">– ( / +</td>

   <td width="298"></td>

  </tr>

  <tr>

   <td width="58">)</td>

   <td width="162">Pop stack</td>

   <td width="141">3 4 2 * 1 5 –</td>

   <td width="60">/ +</td>

   <td width="298">Pop and append operators until opening parenthesis;then pop opening parenthesis</td>

  </tr>

  <tr>

   <td width="58">^</td>

   <td width="162">Push ^ to stack</td>

   <td width="141">3 4 2 * 1 5 –</td>

   <td width="60">^ / +</td>

   <td width="298">^ has higher precedence than /</td>

  </tr>

  <tr>

   <td width="58">2</td>

   <td width="162">Append 2 to expression</td>

   <td width="141">3 4 2 * 1 5 – 2</td>

   <td width="60">^ / +</td>

   <td width="298"></td>

  </tr>

  <tr>

   <td width="58">^</td>

   <td width="162">Push ^ to stack</td>

   <td width="141">3 4 2 * 1 5 – 2</td>

   <td width="60">^ ^ /+</td>

   <td width="298">^ is evaluated right-to-left</td>

  </tr>

  <tr>

   <td width="58">3</td>

   <td width="162">Append 3 to expression</td>

   <td width="141">3 4 2 * 1 5 – 2 3</td>

   <td width="60">^ ^ /+</td>

   <td width="298"></td>

  </tr>

  <tr>

   <td width="58"><em>end</em></td>

   <td width="162">Pop entire stack to output</td>

   <td width="141">3 4 2 * 1 5 – 2 3 ^^ / +</td>

   <td width="60"></td>

   <td width="298"></td>

  </tr>

 </tbody>

</table>




<strong>            </strong>

<h2>Converting Prefix Expressions (PN) to Postfix (RPN)</h2>







<ul>

 <li>Read the Prefix expression in reverse order (from right to left) When an operand is encountered, push it onto the stack</li>

 <li>When an operator is encountered:

  <ul>

   <li>Pop two operands/strings from the stack: op1 = pop(), op2 = pop()</li>

   <li>Create a string by concatenating the two operands/strings and the operator after them: string = op1 + op2 + operator (remember space separation)</li>

   <li>Push the resultant string back to the stack</li>

  </ul></li>

 <li>Repeat the above steps until end of Prefix expression</li>

 <li>The one string remaining on the Stack is the resultant Postfix expression</li>

</ul>







For example, given the Prefix expression: * – 3 / 2 1 – / 4 5 6




<table width="0">

 <tbody>

  <tr>

   <td width="58"><strong>Input</strong></td>

   <td width="342"><strong>Action</strong></td>

   <td width="133"><strong>Stack</strong></td>

   <td width="185"><strong>Notes</strong></td>

  </tr>

  <tr>

   <td width="58">6</td>

   <td width="342">Push ‘6’ onto stack</td>

   <td width="133">‘6’</td>

   <td width="185">Read from right to left</td>

  </tr>

  <tr>

   <td width="58">5</td>

   <td width="342">Push ‘5’ onto stack</td>

   <td width="133">‘5’ ‘6’</td>

   <td width="185"></td>

  </tr>

  <tr>

   <td width="58">4</td>

   <td width="342">Push ‘4’ onto stack</td>

   <td width="133">‘4’ ‘5’ ‘6’</td>

   <td width="185"></td>

  </tr>

  <tr>

   <td width="58">/</td>

   <td width="342">Pop ‘4’, ‘5’, combine with /, push onto stack</td>

   <td width="133">‘4 5 /’ ‘6’</td>

   <td width="185">Keep tokens space separated</td>

  </tr>

  <tr>

   <td width="58">–</td>

   <td width="342">Pop ‘4 5 /’, ‘6’, combine with -, push onto stack</td>

   <td width="133">‘4 5 / 6 -’</td>

   <td width="185"></td>

  </tr>

  <tr>

   <td width="58">1</td>

   <td width="342">Push 1 onto stack</td>

   <td width="133">‘1’ ‘4 5 / 6 -’</td>

   <td width="185"></td>

  </tr>

  <tr>

   <td width="58">2</td>

   <td width="342">Push 2 onto stack</td>

   <td width="133">‘2’ ‘1’ ‘4 5 / 6 -’</td>

   <td width="185"></td>

  </tr>

  <tr>

   <td width="58">/</td>

   <td width="342">Pop ‘2’,’1’, combine with /, push onto stack</td>

   <td width="133">‘2 1 /’ ‘4 5 / 6 -’</td>

   <td width="185"></td>

  </tr>

  <tr>

   <td width="58">3</td>

   <td width="342">Push 3 onto stack</td>

   <td width="133">‘3’ ‘2 1 /’ ‘4 5 / 6-’</td>

   <td width="185"></td>

  </tr>

  <tr>

   <td width="58">–</td>

   <td width="342">Pop ‘3’,‘2 1 /’, combine with -, push onto stack</td>

   <td width="133">‘3 2 1 / -’ ‘4 5 / 6-’</td>

   <td width="185"></td>

  </tr>

  <tr>

   <td width="58">*</td>

   <td width="342">Pop ‘3 2 1 / -’,‘4 5 / 6 -’, combine with *, push onto stack</td>

   <td width="133">‘3 2 1 / – 4 5 / 6 –*’</td>

   <td width="185"></td>

  </tr>

  <tr>

   <td width="58"><em>end</em></td>

   <td width="342">Pop entire stack to output</td>

   <td width="133"></td>

   <td width="185">Result: ‘3 2 1 / – 4 5 / 6 – *’</td>

  </tr>

 </tbody>

</table>




<h1>3. Tests</h1>

<ul>

 <li>Write sufficient tests using unittest to ensure full functionality and correctness of your program.</li>

 <li>Make sure that your tests test each branch of your program and any edge conditions. You do not need to test for correct input in the assignment, other than what is specified above.</li>

 <li>postfix_eval(input_str) should raise a ValueError if a divisor is 0. postfix_eval(input_str) should raise a PostfixFormatException if the input is not well-formed.  Specifically, it should raise this exception with the following messages in the following conditions:

  <ul>

   <li>“Invalid token” if one of the tokens is neither a valid operand nor a valid operator.</li>

   <li>“Insufficient operands” if the expression does not contain sufficient operands. o “Too many operands” if the expression contains too many operands.</li>

   <li>Note: to raise an exception with a message: rasie PostfixFormatException(“Here is a message”)</li>

  </ul></li>

 <li>You may assume that when infix_to_postfix(input_str) is called that input_str is a well formatted, correct infix expression containing only numbers, the specified operators, parentheses () and that the tokens are space separated. You may use the Python functions split and join.</li>

 <li>You may assume that when prefix_to_postfix(input_str) is called that input_str is a well formatted, correct prefix expression containing only numbers, the specified operators, and that the tokens are space separated. You may use the Python functions split and join.</li>

</ul>

postfix_eval(input_str) should raise a ValueError if a divisor is 0