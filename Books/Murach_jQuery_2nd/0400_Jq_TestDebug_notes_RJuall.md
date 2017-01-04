# How to Test and Debug a Javascript or jQuery Application

*Murach's Jquery, 2nd Edition*

*Zak Ruvalcaba and Anne Boehm*

page 133

***

## An Introduction to Testing and Debugging

*testing* an application means using/running it to see that it works correctly, attempting to break it to see where problems live.

*debugging* is fixing errors that arise in code

After debugging, more testing must occur

*Syntax errors* occur when the rules of a coding language are not followed

*Runtime errors* occur after compilation/interpretation and result in thrown errors or exeptions, often the result of bad input

*Logic errors* occur because the code was inappropriately designed and does not produce the desired result

Common Errors:

    1. Misspelling keywords
    2. Omitting required parentheses, quotation marks, or braces
    3. Not using the same opening and closing quotation mark
    4. Omiting the semicolon at the end of a statement
    5. Misspelling or incorrectly capitalizing an identifier
    6. Referring to an attribute incorrectly
    7. Not testing input
    8. Not casting to a numerical value when appropriate
    9. Not using 2 equal signs for comparison
    10. Floating point errors
    11. Not using strict mode/global variable errors

*top-down testing* tests a small portion of code at a time, from most to least important

## How to Debug with Chrome's Developer Tools

Error messages show up in the console, also shows the line of code where the error occurs

Breakpoints and stepping through code can be used to solve serious debugging issues

## Other Debugging Methods

IE's developer tools can be used to emulate older versions of IE

*tracing* the execution of code can be accomplished by adding console.logs into the code to see what order they appear in

The 'Elements' panel in Chrome Dev Tools will show the changes made to the DOM

Sometimes an error in HTML can cause errors in Javascript execution

***

### END CHAPTER

Robert Juall

31OCT2016