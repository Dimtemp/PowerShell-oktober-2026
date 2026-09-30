# 2 Sort Filter Group

PowerShell kan data uit verschillende bronnen ophalen en manipuleren. In deze module leer je:
- Sort-Object: sorteren van data op een bepaalde eigenschap.
- Where-Object: filteren op specifieke criteria.
- Group-Object: groeperen van data om patronen of totalen te zien.
Praktisch voorbeeld: Een lijst van auto's sorteren op kenteken, filteren op vermogen en groeperen op bouwjaar.

# PowerShell pipeline basics

Note: as with most PowerShell exercises, it's best not to copy-paste the command's, but to actually type them. Use keyboard navigation (arrow up/down, home, end) to speed up entering commands in PowerShell.


## Task: Sorting
1. Open a PowerShell console.
1. Run this command: ```Get-Process```
1. This will display a process listing. Notice it is sorted alphabetically on ProcessName.
1. Run this command: ```Get-Process | Sort-Object Id```
1. Notice that the process listing is sorted on the Id column.
1. Run this command: ```Get-Process | Sort-Object Id -Descending```
1. Notice that the process listing is sorted descending on the Id column.
1. Run this command: ```Get-Process | Sort Id```
1. The result is sorted on the id column. Please notice the use of the sort alias instead of the Sort-Object cmdlet. Many commands that have a **Object** Noun, an alias exists without the noun. For example, Sort is an alias for Sort-Object, Measure is an alias for Measure-Object.



# Filtering with and without Where-Object
In this section we're going to filter output.

## Task: basic filtering
1. Run this command: ```Get-Help operators```
1. If this command does not produce helpfull output, try running this command to update the help files: ```Update-Help```.
1. PowerShell has several helpfiles covering the use of operators.
1. Run this command: ```Get-Help about_Operators```
1. This is a help article about operators in general.
1. Run this command: ```Get-Help about_Comparison_Operators```
1. This is a help article about comparison operators.
1. Run this command: ```Get-Process```
1. This displays a list of all running processes. Notice the Handles column.
1. Run this command: ```Get-Process | Where-Object Handles -GT 1000```
1. This displays a list of all running processes that have more than 1000 handles.
1. Run this command: ```Get-Process | Where-Object Handles -LT 1000```
1. This displays a list of all running processes that have less than 1000 handles.
1. Run this command: ```Get-Service```
1. This displays a list of all services.
1. Run this command: ```Get-Service | Where-Object Status -EQ Running```
1. This displays a list of all services that are running.
1. Run this command: ```Get-Service | Where-Object Status -EQ Stopped```
1. This displays a list of all services that are not running.


## Task: like this
1. Run this command to display only processes that start with **w**: ```Get-Process | Where-Object name -LIKE w*```
1. This should list several processes with their names starting with a **w**.
1. Run this command to display only processes that have **svc** in their name:
1. ```Get-Process | Where-Object name -LIKE *svc*```
1. Run this command to display only processes that end with **s**:
1. ```Get-Process | Where-Object name -LIKE *s```


## Task: match that
PowerShell has an extremely **PowerFull** pattern matching mechanism: regular expressions. Originating not earlier than **1951**, it's a wonderfull way to describe patterns in input and output.

1. Run this command to list all processes that have **sh** in their names: ```Get-Process | Where-Object ProcessName -match sh```
1. Notice that we're not using any wildcards, like * or ?.
1. Note: if you don't get any output, try to use another text until you get a (preferred small) result.
1. Run this command to list all services that have **win** in their names: ```Get-Service | Where-Object Name -match win```
1. The most basic way of using operators, like the -MATCH operator, is without any cmdlet or function. Like this:
1. ```'Rick' -MATCH "[DMNR]ick"```
1. This command results in true, because **Rick** matches the regular expression **[DMNR]ick**. The brackets **[]** let any character match in that position, after which the string mus continue with **ick**. Try these combinations:
1. ```'Dick' -MATCH "[DMNR]ick"```
1. ```'Mick' -MATCH "[DMNR]ick"```
1. ```'Nick' -MATCH "[DMNR]ick"```
1. ```'Sick' -MATCH "[DMNR]ick"```
Only **Sick** results in false, because the **S** is not part of the **DMNR** collection.


## Task: filtering at the source
The Where-Object has a major advantage: all PowerShell output can be filtered. It also has a huge disadvantage: all output will be filtered locally, by PowerShell. Some commands allow to filter at the source. This can prevent huge data transfers across the network, or can help speed up processing.
1. ```Get-Process -Name *sys*```
1. This command filters all processes with **sys** in it's name. This filter is executed at the source.
1. Run this command: ```Get-ChildItem -Path C:\Windows -Filter *.exe```
1. You might get no results, depending on your PC. The command should filter only files with an .EXE extension.
1. Run this WMI command: ```Get-CimInstance -Class win32_service -Filter "Name='spooler'"```
1. Notice the exact use of the quotes, the previous command includes four quotes in total: two double quotes and two single quotes.


## Task: Grouping
1. Run this command: ```Get-Command```
1. This will display a listing of all commands in PowerShell. Notice the header of the table: all command's have a specific **CommandType**.
1. Run this command: ```Get-Command | Group-Object CommandType```
1. This will group all commands by CommandType. Notice that most commands are either a Function or a Cmdlet.
1. Retrieve a service listing by running this command: ```Get-Service```
1. Notice that all services have a status. Most are running or stopped.
1. Run this command: ```Get-Service | Group-Object Status```
1. This will group all services by Status. Notice that most services are either running or stopped.
1. The Count column specifies the number of services with a specific status. The Name column does not refer to the service name, but to the name of the status. Most will be Stopped or Started. The Group column contains all services with a specific status. The curly brackets { } indicate it's a collection of objects.


# The many faces of Select-Object
The Select-Object command is one of the most popular commands in Powershell. It can be used in four different ways. Let's take a look in each of them.

Note: as with most PowerShell exercises, it's best not to copy-paste the command's, but to actually type them. Use keyboard navigation (arrow up/down, home, end) to speed up entering commands in PowerShell.

## Task: Selecting properties
1. Run the following command to view all processes with a name that start with **w**. This should produce a short list.
1. ```Get-Process w*```
1. Run the following command to view the previous processes, but only with a few specific properties: Id and ProcessName.
1. ```Get-Process w* | Select-Object Id, ProcessName```
1. Run the following command to view the previous processes, but with other properties:
1. ```Get-Process w* | Select-Object WS, Id, ProcessName```


## Task: The first will be last
1. The First and Last parameters of Select-Object can return a shorter list so you can focus on the biggest or smallest items. For example: disk space, memory usage, network bandwidth.
1. Run this command to display the first 10 processes: ```Get-Process | Select-Object -First 10```
1. Notice only 10 processes are returned.
1. ```Get-Process | Select-Object -Last 10```
1. Notice that the process listing is sorted alphabetically. We'll sort on workingset (WS), which gives an indication on memory usage.
1. ```Get-Process | Sort-Object WS | Select-Object -First 10```
1. This command produces a list with processes that have the least memory usage. Let's produce a list with the most memory intensive applications:
1. ```Get-Process | Sort-Object WS | Select-Object -Last 10```
1. By default sorting in PowerShell is performed ascending: 0..9, A..Z. You can also choose to sort the list descending. This gives a nice result combined with the -First parameter of Select-Object:
1. ```Get-Process | Sort-Object WS -Descending | Select-Object -First 10```
1. Also notice that most parameters can be abbreviated:
1. ```Get-Process | Sort-Object WS -Desc | Select-Object -First 10```
1. The previous example contains two commands that are generally abbreviated. The following command is not a recommended practice, but it works the same:
1. ```Get-Process | Sort WS -Desc | Select -Last 10```


## Task: The expanding universe
1. The ExpandProperty parameter of Select-Object can display truncated or hidden information.
1. Display the PowerShell version information: ```$Host```
1. Notice the Version. Now display only the version using Select-Object:
1. ```$Host | Select-Object Version```
1. Notice the Version. It displays in the same way as the first command.
1. Now display the version using the ExpandProperty of Select-Object: ```$Host | Select-Object -ExpandProperty Version```
1. You'll notice extra information was hidden inside the version property.


## Filter left, format right.
A famous paradigm in PowerShell is: **filter left, format right**. This means you should filter output as soon as possible. At the source, when available. Filtering using Where-Object is flexbile, but also more costly in terms of processing time and/or network transfers.

Formatting is done on the right. To be precise: in the last part of your PowerShell command. This will be discussed in a later chapter.


## If time permits

## Task: Measuring
1. Open a PowerShell console.
1. Run this command: ```Get-Command```
1. This will display a listing of all commands in PowerShell.
1. Run this command: ```Get-Command | Measure-Object```
1. This command measures the number of command's in PowerShell. Notice the total number of commands.
1. Run this command: ```Get-Command -verb stop```
1. This will display a listing of all commands in PowerShell that have a verb of **stop**.
1. Run this command: ```Get-Command -verb stop | Measure-Object```
1. This command measures the number of command's in PowerShell that have a verb of **stop**. Notice the total number of commands.
1. Run this command: ```Get-Process```
1. This will display a process listing.
1. Run this command: ```Get-Process | Measure-Object```
1. This command measures the number of processes.
1. Run this command: ```Get-Process w*```
1. This command displays a list of processes with a name that starts with **w**. Count the number of processes.
1. Run this command: ```Get-Process w* | Measure-Object```
1. This command measures the number of processes with a name that starts with **w**. Verify that the number is correct.


