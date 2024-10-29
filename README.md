java cComputation and Programming 
2024 
Project – Playing with Hailstone Numbers 
The project has two parts: 
• Building a program that allows the user to explore some features of the number sequences 
related to the Collatz Conjecture. 
• The implementation of a simple game related to the Collatz conjecture. 
 
The Collatz Conjecture 
The Collatz Conjecture (named after Lothar Collatz, who introduced it in 1937), also known as the 3x+1 
problem, states that, starting with any positive integer, x, and applying two simple operations (if the 
number is even, divide it by 2; if the number is odd, multiply it by 3 and add 1), number 1 will eventually 
be reached. 
In a more rigorous way, we can define the Collatz function, C, as: 
And so, the Collatz Conjecture states that “starting from any positive integer n, iterations of the function 
C(x) will eventually reach the number 1”. 
Some examples: 
• Starting with 6, we get the sequence: 6 - 3 - 10 - 5 - 16 - 8 - 4 - 2 - 1 
• Starting with 7: 7- 22 - 11 - 34 - 17 - 52 - 26 - 13 - 40 - 20 - 10 - 5 - 16 - 8 - 4 - 2 – 1 
• Starting with 13: 13 – 40 – 20 – 10 – 5 – 16 – 8 – 4 – 2 – 1 
• Starting with 15: 15 - 46 - 23 - 70 - 35 - 106 - 53 - 160 - 80 - 40 - 20 - 10 - 5 - 16 - 8 - 4 - 2 – 1 
• Starting with 84: 84 – 42 – 21 – 64 – 32 – 16 – 8 – 4 – 2 – 1 
Note that these sequences are infinite (looping 1-4-2-1-4-2-1-4-2-1-…), but we are only considering them 
until number 1 is reached for the first time. 
One of the interesting things about this conjecture is that, although very simple to characterize, it has 
never been proved. But we can explore some of these sequences and try to discover some curious things 
about these hailstone numbers (another name for the numbers in these sequences).  CP 2024 - Project 
CP 2024 – Project – Playing with hailstone numbers 2 
 
1. Exploring [70 points] 
In this first part, you must build a program that presents a Main Menu and allows the user to choose one 
of the options. Each option corresponds to some experiment regarding the sequences of hailstone 
numbers. 
The presentation of the main menu may be similar to the following. 
****** Main Menu ****** 
 
 1 - Display a sequence 
 2 - Display a sequence + properties 
 3 - Display bar chart for a range of numbers 
 4 - Test Benford's law for one number 
 5 - Test Benford's law for a range 
 9 - Exit the program 
 
Which option? 
The description of what is the expected behavior for each option is detailed in the following sections. 
After executing the chosen option, the menu should be presented again. The program should end when 
the user chooses option 9 (exit). 
Option 1 – Display a sequence 
In this option the user should have the possibility of choosing a number and the program should present 
its trajectory (the sequence until 1 is reached). For instance: 
Which option? 1 
 
Enter a number (<= 100000): 17 
 
The trajectory for 17 is: 
17 - 52 - 26 - 13 - 40 - 20 - 10 - 5 - 16 - 8 - 4 - 2 - 1 
To accomplish this, you should start by defining a function next that, given a number, returns the next 
number in the sequence. Consider this prototype: 
long next(long number) ; 
Then, you can define a function, printSequence, to print the trajectory generated for the given 
number: 
void printSequence(long number) ; 
  CP 2024 - Project 
CP 2024 – Project – Playing with hailstone numbers 3 
 
Option 2 – Display a sequence and its properties 
Besides presenting the trajectory, like in the previous option, here the program should also present some 
of its properties, namely: 
• Its height (the number of elements in the trajectory, until it reaches 1). 
• Its stopping time (the first step at which the number in the sequence gets smaller than the 
original number). 
• The maximum number in the trajectory. 
• The number of odd numbers in the trajectory. 
• The maximum number of consecutive even numbers. 
Start by defining a function, buildSequence, that, given a number, generates a sequence, stores it in 
an array and returns its size (height). Then, build a function, displaySequenceProperties, that 
takes a sequence and its size and displays the sequence and all the above-mentioned properties. 
Consider the following prototypes for these functions: 
int buildSequence(long number, long seq[]); 
void printSeqProperties(long sequence[], int size); 
The expected behavior for this option is similar to the following: 
Which option? 2 
 
Enter a number (<= 100000): 19 
 
The trajectory for 19 is: 
19 - 58 - 29 - 88 - 44 - 22 - 11 - 34 - 17 - 52 - 26 - 13 - 40 - 20 - 10 - 5 
- 16 - 8 - 4 - 2 – 1 
 
 Height: 21 
 Stopping time: 7 
 Maximum number in trajectory: 88 
 Number of odd numbers in trajectory: 7 
 Maximum consecutive even numbers: 4 
Note that the trajectory has 21 elements, the first element smaller than 19 is the 7
th
 (11), the maximum 
number that occurs is 88, there are 7 odd numbers (19, 29, 11, 17, 13, 5, and 1) and the longest 
sequence of consecutive even numbers has size 4 (16-8-4-2, near the end). 
Option 3 – Display stats for a range of numbers 
In this option, the user should be asked for two numbers that define a non-empty range (the second 
must be greater or equal than the first). 
Then, the program must present a horizontal bar chart that includes, for each line (each number in the 
range): 
• The number 
• The height of its trajectory 
• A bar with stars (‘*’) representing that height.  CP 2024 - Project 
CP 2024 – Project – Playing with hailstone numbers 4 
 
Besides, as there is a great disparity between the lengths of different numbers, the bars should be 
scaled, if necessary, so that they fit in 50 columns (or whatever other limit you define) maintaining their 
relative proportionality. 
An example of the expected behavior: 
Which option? 3 
Enter the two integer numbers that define the range: 235 250 
 
Number | Height | Bar 
 
Option 4 – Test the Benford’s Law 
In many real-life sets of numbers, the distribution of the leading digit (most significant one) follows a 
particular distribution: 
 
According to this distribution, number 1 occurs as a leading digit 30.1% of the times, number 2, 17.6%, 
and so on (exact definition bellow). This is called the Benford’s Law (named after Frank Benford, who 
stated it in 1938). This law states that when a set of numbers follows it, the probability of a digit d (d  
{1, 2, …, 9}) appearing as a leading one is given by 
  (  ) = log10 (1 +
1
  
)  CP 2024 - Project 
CP 2024 – Project – Playing with hailstone numbers 5 
 
In this option your program should apply the Goodness of Fit test to verify that the hailstone numbers 
follow the Benford’s law. 
The program should do the following: 
• Ask for a number 
• Present its trajectory 
• Present the digits counting (how many times each digit appears in the first position) 
• Verify if the 
2
 Goodness of fit test can be applied to verify if the observed distribution of digits 
follows Benford’s Law. 
o (refer to slide 28, part VII, of the Probability and Statistics course) 
• If the test cannot be applied, just print a message. 
• If the test can be applied, calculate the T statistics, and decide to reject (or not) the null 
hypothesis (H0: the observations follow the distribution of the Benford’s Law) with a confidence 
of 95%. 
Let’s see two examples of the e代 写program、c/c++
代做程序编程语言xpected behavior. The first, for a number for which its trajectory does not 
have enough elements to apply the test: 
Which option? 4 
 
Enter a number (<= 100000): 19 
 
The trajectory for 19 is: 
19 - 58 - 29 - 88 - 44 - 22 - 11 - 34 - 17 - 52 - 26 - 13 - 40 - 20 - 
10 - 5 - 16 - 8 - 4 - 2 - 1 
 
Digit counting and percentages 
1 - 7 - 33.33 
2 - 5 - 23.81 
3 - 1 - 4.76 
4 - 3 - 14.29 
5 - 3 - 14.29 
6 - 0 - 0.00 
7 - 0 - 0.00 
8 - 2 - 9.52 
9 - 0 - 0.00 
The sequence for number 19 does not satisfy the applicability 
conditions. 
 
 
 
 
 
 
  CP 2024 - Project 
CP 2024 – Project – Playing with hailstone numbers 6 
 
Now an example for which the test can be applied: 
Which option? 4 
 
Enter a number (<= 100000): 31 
 
The trajectory for 31 is: 
31 - 94 - 47 - 142 - 71 - 214 - 107 - 322 - 161 - 484 - 242 - 121 - 364 
- 182 - 91 - 274 - 137 - 412 - 206 - 103 - 310 - 155 - 466 - 233 - 700 
- 350 - 175 - 526 - 263 - 790 - 395 - 1186 - 593 - 1780 - 890 - 445 - 
1336 - 668 - 334 - 167 - 502 - 251 - 754 - 377 - 1132 - 566 - 283 - 850 
- 425 - 1276 - 638 - 319 - 958 - 479 - 1438 - 719 - 2158 - 1079 - 3238 
- 1619 - 4858 - 2429 - 7288 - 3644 - 1822 - 911 - 2734 - 1367 - 4102 - 
2051 - 6154 - 3077 - 9232 - 4616 - 2308 - 1154 - 577 - 1732 - 866 - 433 
- 1300 - 650 - 325 - 976 - 488 - 244 - 122 - 61 - 184 - 92 - 46 - 23 - 
70 - 35 - 106 - 53 - 160 - 80 - 40 - 20 - 10 - 5 - 16 - 8 - 4 - 2 - 1 
 
Digit counting and percentages: 
1 - 30 - 28.04 
2 - 17 - 15.89 
3 - 14 - 13.08 
4 - 15 - 14.02 
5 - 7 - 6.54 
6 - 5 - 4.67 
7 - 7 - 6.54 
8 - 5 - 4.67 
9 - 7 - 6.54 
 
Tstat = 4.385 
H0 is not rejected. 
According to the Chi-Squared distribution table, with 8 degrees of freedom, and a significance level (α) of 
0.05, H0 is rejected when the value of the T statistics is greater than 15.507. 
  CP 2024 - Project 
CP 2024 – Project – Playing with hailstone numbers 7 
 
Option 5 – Test the Benford’s Law for a range 
In this option, the program must present aggregate results regarding the applicability of the Goodness of 
Fit test and its results for the digits distribution of the hailstone sequences for a range of numbers 
provided by the user. 
So, the program must: 
• Ask the user for the two integers that define the range. 
• Calculate the values to be presented. 
• Display the following aggregate results: 
o Number of values in the range for which the Goodness of fit test can be applied 
o Number of values for which the value of the statistics means that the H0 is not rejected. 
o Average value of the T statistics 
An example: 
Which option? 5 
 
Enter two integer numbers: 1 100000 
 
The test can be applied for 51873 numbers ( 51.8730%). 
The null hypothesis is not rejected for 51871 of those numbers ( 99.9961%). 
The average value of the statistics is 3.485. 
Another example: 
Which option? 5 
Enter two integer numbers: 1000 2000 
The test can be applied for 328 numbers ( 32.7672%). 
The null hypothesis is not rejected for 328 of those numbers (100.0000%). 
The average value of the statistics is 3.555. 
 
 
2. Playing [30 points] 
The second program of your project is the implementation of a very simple game. 
The game consists of guessing the next number in the Collatz sequence, given a number randomly 
generated by the computer. The game should have the following properties: 
• The program must ask first for the range from which to generate the random numbers. 
• Then, the program must ask for a limit in the number of plays. 
• The game begins and in each play: 
o The program presents to the user a randomly generated number . 
o The user should guess the number that follows the number presented, according to the 
Collatz function. 
o The program presents the result (the guess was correct or not) and asks the user if 
he/she wants to play another time or end the game.  CP 2024 - Project 
CP 2024 – Project – Playing with hailstone numbers 8 
 
• When the game ends, either because the limit of plays was reached or because of the user 
choice, the results should be presented. These include: 
o The total number of guesses 
o The number of correct guesses 
o The score (percentage of correct guesses) 
o The list of numbers for which the user failed to guess 
An example: 
Let's play a game! 
******************* 
 
Enter two integers representing the range of possible values 
to be randomly generated by the program: 50 100 
 
Enter the maximum number of plays: 3 
(You can end before, by answering "no" when asked for another try.) 
 
***** Let's START **** 
The number is 82. 
What is the next number? 41 
CORRECT! 
 
Another try (write "no" to stop)? y 
The number is 97. 
What is the next number? 292 
CORRECT! 
 
Another try (write "no" to stop)? y 
The number is 71. 
What is the next number? 214 
CORRECT! 
 
The maximum number of plays have been reached. Let's see your results! 
 
Results 
+++++++ 
 
 Games Played: 3 
 Games Won: 3 
 Your Score: 100.00% 
 
Congratulations!! You guessed all numbers correctly!  CP 2024 - Project 
CP 2024 – Project – Playing with hailstone numbers 9 
 
Another example of execution: 
Let's play a game! 
******************* 
 
Enter two integers representing the range of possible values 
to be randomly generated by the program: 1 100000 
 
Enter the maximum number of plays: 20 
(You can end before, by answering "no" when asked for another try.) 
 
***** Let's START **** 
 
The number is 31496. 
What is the next number? 15748 
CORRECT! 
 
Another try (write "no" to stop)? y 
The number is 26593. 
What is the next number? 79780 
CORRECT! 
 
Another try (write "no" to stop)? y 
The number is 26711. 
What is the next number? 80133 
Incorrect! The number after 26711 is 80134. 
 
Another try (write "no" to stop)? y 
The number is 3297. 
What is the next number? 9892 
CORRECT! 
 
Another try (write "no" to stop)? y 
The number is 31926. 
What is the next number? 15963 
CORRECT! 
 
Another try (write "no" to stop)? y 
The number is 26449. 
What is the next number? 78348 
Incorrect! The number after 26449 is 79348. 
 
Another try (write "no" to stop)? no 
 
Results 
+++++++ 
 
 Games Played: 6 
 Games Won: 4 
 Your Score: 66.67% 
You failed to guess the next for the following numbers: 
26711 26449 
  CP 2024 - Project 
CP 2024 – Project – Playing with hailstone numbers 10 
 
Final Remarks 
Submitting your work 
Projects should be done in groups of 4 students. 
You should submit a zip file containing: 
• Your two programs (two files: collatz-main.c and collatz-game.c) 
o These two files should include, as comments, the student numbers and names of the 
elements of the group 
• A document containing the identification of the group. For each member of the group, you 
should identify: 
o Student number 
o Chinese name 
o Name in English 
• A document with a copy of the execution of the program (copy/paste of the output) 
Submission is made through the elearning platform in a link that will be provided in a few days. 
It is enough that one of the elements of the group submits the zip file. 
Deadline for submission: 
27 October 2024 
 
         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
