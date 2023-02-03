# Execution and Development Environment
To complete this project, I used Visual Studio Code on my Macbook M1 pro.
# Compilation Result
Using the terminal, I used the following commands on the project files:

> javac lexer/setup/TokenSetup.java

> java lexer.setup.TokenSetup

> javac lexer/Lexer.java

> java lever.Lexer filename.x

The program ran as expected and no error messages were displayed
# Assumptions
I assumed that the file entered from the command line exists and is an x file. I also assumed
that all timestamp elements will have trailing zeros behind numbers less than 4 or 2 digits
(i.e. 0001 for year and 04 for month). Any other illegal or invalid characters and tokens inside
the x file will be thrown away by the error handling.
# Implementation
## Output design
After studying the lexer class and its associated classes and files, I began to slowly understand
the gist of how everything is operating. To improve the output, I knew I needed to move
everything away from the main method and into a lexer toString. However, before doing that I
tried to place the previous implementation of the output inside a for loop that takes an
argument in the form of a String, or in this case, a file path.
After implementing a way to dynamically type and scan a file directly from the command line, I
began to organize the output to the desired format inside the toString. I used String.format to
create a consistent design for scanned tokens that shows all required information. To track the
line number and use it in the output information, I created an instance variable and a getter
method inside the lexer class.
Finally, to print the raw code upon successful completion of lexical analysis, I added the read
lines during the analysis to a string and printed the string at the end of the output specifying
each line.
## New Token types and reserved keywords
This was one of the easier tasks in the implementation of this project. All I needed to do was
add the token identifiers and their corresponding names to the tokens file, run the TokenSetup
class and the tokens were automatically added to the Tokens and TokenType classes.
## New Utf16StringLit token
For the implementation of this token literal, I knew I needed to check each half of the string
separately with the “\” as the halfpoint. Therefore, Inside the nextToken() method in the lexer
class I created a new try->catch block that runs after a “\” is encountered. My implementation
is simply a while loop that runs until a “\” is encountered, otherwise, it keeps scanning the next
token. Within that while loop, I created a nested while loop for when the second “\” is
encountered that checks the second half of the utf16String. I equipped each while loop with
their own error checking conditions such as length and character value.
## New TimeStampLit token
For the implementation of the TimeStampLit token, I created a helper method named,
“timeCalc” that takes a String token, an integer index (String index at which a ‘~’ or ‘:’ are in
the correct position in the token String), two integers “from” and “to” that hold the range of
each element in the TimeStampLit token, and a char symbol that holds the symbol that is
required to be at the index parameter. Next, I simply created a condition inside the digit
checking algorithm within the nextToken() method that only executes if the character after a
4-digit number is a ‘~’. If this condition is met, then a switch statement that takes the length of
the token and checks each important interval inside the token using the timeCalc() method.
# Code Organization
To prevent repetition and code clutter I created the illegalch() and timeCalc() methods inside
the lexer class. This also helped me debug more efficiently.
