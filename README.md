# CS330-PLP

PLP-01:

Microsoft Powershell
Created on November 14, 2006 by Jeffery Snover and his team in Los Angeles at the Professional Developers Conference in 2003, under the name of Monad, which would later be developed and renamed to Powershell. When it was first developed it was purposed to be a better way to manage command lines. It's primarily used to automate tasks but is also used for system administration, configuration management, and cybersecurity efforts, to which users can parse the windows event log and look for a specific type of error or threat. I will primarily get information on how to use Powershell through learn.microsoft and looking at the articles on Powershell, but also website such as Stackoverflow will be helpful throughout this process.

The language comes installed on all Windows processes, so I didn't download anything, but Mac and Linux users would have to download from the Microsoft website. It comes as it's own client, so you dont need to worry about different programming environments. You run program by running the file directly through powershell or calling it's full path. For single line comments its # and for multi-line comments you do <# *insert text comments* #>.

PLP-02:

Powershell applies a verb-noun naming convention cmdlets, functions, and scripts (ex: remove-item). Within Powershell, variable names can include numbers, letters, and underscore. They cannot have spaces or special characters apart from underscores. Variable names are case-insensitive, but it's believed to be good practice to act as if they're case-sensitive. They use both CamelCase (first letter is lowercase then next word is uppercase in a variable ex: myVariable) and PascalCase (first letter of each word is capitalized ex: MyVariable)

Powershell does offer a decent amount (13 total) of keywords and reserved words such as "if", "else", "function", and "switch". Powershell is a dynamically typed language, which means variables don't have a fixed operand type and they can be changed throughout runtime. Powershell is a weakly typed language which means the variables are loosely defined and their types can change at runtime. If explcitly defined, Powershell can also support strong typing. You can choose to make some variables mutable, but they are inherently immutable. Mixed-type operations are allowed in Powershell, it automatically will perform type conversations to accomodate for mixed-type operations. Identifier names and operator symbols are bound at runtime in Powershell. Powershell does have certain limitations such as a restricted command set, scripting limitations, compatibility with 3-rd party clients, and resource management. The built-in complex data types powershell supports are arrays, hash tables, and custom objects.

Sources: https://powershellfaqs.com/powershell-variable-naming-conventions/

PLP-03:

Boolean values in Powershell are $true and $false, but PowerShell also implicitly converts various values to booleans, true values consist of:
- Any non-zero number
- Any non-empty string
- Any non empty collection
- Any object that isn't $null

While false values consist of:
- the number 0
- any empty string ("")
- An empty collection
- $null

Sources: https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_booleans?view=powershell-7.5

In PowerShell, the conditional statements available are if and else statements, elseif statements, logical operators of and, or, and not, and ternary operators (greater than, lesser than, equal to, and not equal to.) PowerShell also offers switch statements and null checks. PowerShell also offers "like" statements which are for wildcard patterns and a match operator for regular expressions.

Sources: https://learn.microsoft.com/en-us/powershell/scripting/learn/deep-dives/everything-about-if?view=powershell-7.5

PowerShell uses curly brackets as block delimiters in selection control statements (ex: if (condition){
(statements
})

PowerShell uses short-circuit evaluation by only checking if the initial condition works for most code as seen in this code taken from Stack Overflow below:

PS C:\> 1 -eq 0 -or $(Write-Host 'foo')
foo
False
PS C:\> 1 -eq 1 -or $(Write-Host 'foo')
True

PS C:\> 1 -eq 1 -and $(Write-Host 'foo')
foo
False
PS C:\> 1 -eq 0 -and $(Write-Host 'foo')
False

Sources: https://stackoverflow.com/questions/26766559/how-to-perform-short-circuit-evaluation-in-windows-powershell-4-0

PowerShell doesn't face the "dangling else" problem in a way that other languages would because it's syntax is hard-coded to not leave room for any ambiguity in conditional statements.

In PowerShell the switch statement runs like:
switch (condition){
<result1 to be matched> {<action>}
<result2 to be match> {<action>}
}

Syntax is similar to if statements. Default acts as the else for a switch. The following parameters are set for switch statements:

- Wildcard: indicated that the condition is a wildcard string, if the match isnt a string the parameter is ignored. comparison is case-insensitive
- Exact: indicated that the match must match exactly, if match clause isn't a string the parameter is ignored, case-insensitive still.
- CaseSensitive: performs a case-sensitive match, if clause isn't a string parameter is ignored.
- File: takes input from a file, the file is read a line at a time, case-insensitive.
- Regex: performs a regex pattern match, if the match clause isn't a string the parameter is ignored, case-insensitive.

Break and continue are used in PowerShell switch statements with break ending the switch and continue staying in the switch but no longer processing the current value.

Sources: https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_switch?view=powershell-7.5


PLP-04 Functions:

The syntax for declaring a function in PowerShell is:
function FunctionName {
    # Code to execute
}
with the function init being "function" in lowercase followed by the function name in PascalCase, and all code being encompassed in curly braces.

There are no specific rules about where a function needs to be placed in the code fie to run.

Yes, PowerShell supports recursive functions.

In PowerShell, functions can have an unlimited number of parameters of any different data type.

Yes, multiple values at a time can be returned using data structures such as arrays, hashtables, or custom objects.

PowerShell is pass by reference by default which means if you pass an object to a function or assign it to another variable, any changes made will affect the original object/variable. Although, you can manually override to pass by object by modifying a function.

Depending on the context of the variables/parameters/objects they will be stored in different locations. Arguments are stored in the $args automatic variable if not assigned to anything $args is an array. Parameters are explicity defined so will be help in the object/variable they are defined to. Local variables are stored in the local script they are defined in, and are only available there. Accessible using this cmd: Get-Variable -Scope Local

Source: https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_parameters?view=powershell-7.5

According to the Microsoft Education Forums: "When you start PowerShell, the host (pwsh.exe) creates a PowerShell runspace. Host processes can have multiple runspaces. Each runspace has its own session state and scope containers. Session state and scopes can't be accessed across runspace instances." This means you can have parent-scopes and children-scopes and there is scope heirarchy. Using: Get-Variable -Scope Local you can get all the local variables in the scope, and interchanging Local for Global you can get all the global scopes. Local scopes are only visible and accessible within their curly brace codeblocks, while global variables will have a lifetime of as long as the code is.

Source: https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_scopes?view=powershell-7.5

In PowerShell side effects are possible, such as modifying a variables outside of a function, writing files to external systems, outputting unintended data. These can be avoided by avoiding modifying global and parent scope variables unless necessary, use explicit printing and return verbage, using functional coding syntax to avoid complex side effects.

Source: https://softwareengineering.stackexchange.com/questions/426595/best-practice-to-avoid-unintentional-side-effects-in-powershell-scripts

Parameters in a function are defined inside the curly braces like: 
function Get-Greeting {
Param (
[string]$Name
)
Write-Output "Hello, World!"
}
