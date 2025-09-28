# CS330-PLP

PLP-01:

Microsoft Powershell
Created on November 14, 2006 by Jeffery Snover and his team in Los Angeles at the Professional Developers Conference in 2003, under the name of Monad, which would later be developed and renamed to Powershell. When it was first developed it was purposed to be a better way to manage command lines. It's primarily used to automate tasks but is also used for system administration, configuration management, and cybersecurity efforts, to which users can parse the windows event log and look for a specific type of error or threat. I will primarily get information on how to use Powershell through learn.microsoft and looking at the articles on Powershell, but also website such as Stackoverflow will be helpful throughout this process.

The language comes installed on all Windows processes, so I didn't download anything, but Mac and Linux users would have to download from the Microsoft website. It comes as it's own client, so you dont need to worry about different programming environments. You run program by running the file directly through powershell or calling it's full path. For single line comments its # and for multi-line comments you do <# *insert text comments* #>.

PLP-02:

Powershell applies a verb-noun naming convention cmdlets, functions, and scripts (ex: remove-item). Within Powershell, variable names can include numbers, letters, and underscore. They cannot have spaces or special characters apart from underscores. Variable names are case-insensitive, but it's believed to be good practice to act as if they're case-sensitive. They use both CamelCase (first letter is lowercase then next word is uppercase in a variable ex: myVariable) and PascalCase (first letter of each word is capitalized ex: MyVariable)
