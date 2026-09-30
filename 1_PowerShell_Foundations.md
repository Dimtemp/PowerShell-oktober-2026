# 1 PowerShell Foundations

Dit is de basis van PowerShell, een krachtige command-line tool en scriptingtaal van Microsoft. Je leert:
- Hoe je cmdlets (PowerShell-commando’s) gebruikt.
- Hoe je basiscommando's gebruikt zoals Get-Help en Get-Command
Doel: Begrijpen hoe PowerShell werkt en hoe je het kunt inzetten om repetitieve taken te automatiseren.


## Task: Start PowerShell
1. Rightclick the Windows start button, and click **Run**.
1. Enter **PowerShell** and click OK.
1. On the taskbar, right-click the Windows PowerShell icon and then click **Pin to taskbar**.


## Task: Keyboard navigation
1. In the PowerShell console window, type ```Get-Serv``` and press **Tab** on your keyboard. PowerShell will complete the command to ```Get-Service```.
1. Press Enter. This will display a service listing.
1. In the PowerShell console window, type ```Get-Proc``` and press **Tab**. PowerShell will complete the command to ```Get-Process```.
1. Press Enter. This will display a process listing.
1. In the PowerShell console window, type ```Get-Process -Na``` and press **Tab**. PowerShell will complete the command to ```Get-Process -Name```.
1. Make sure you complete the command to this: ```Get-Process -Name csrss``` and press Enter.
1. This will show a list of processes with the name **csrss**.
1. Press **arrow up** on your keyboard to show the last command.
1. Use the arrow up and down keys to scroll through the last few commands.
1. Press **ESC** on your keyboard to clear the input line.
1. Press **arrow up** to show the last command.
1. Press **home** on your keyboard to set the cursor at the beginning of the command.
1. Press **end** to set the cursor at the end of the command.
1. Press **ESC** again to clear the input line.
1. Finally, long running command's can be cancelled. Try it: ```Sleep 60```. Cancel the command using **Ctrl-C** before the command completes.


## Task: Open the Integrated Scripting Environment (ISE)
1. With the PowerShell console open, type **powershell_ise** and hit Enter.
1. A graphical editor window will open.
1. On the taskbar, right-click the Windows PowerShell ISE icon and then click **Pin to taskbar**.
1. On the Windows PowerShell ISE toolbar, click **View** in the menu bar, and click **Show Script Pane  Ctrl-R**.
1. On the Windows PowerShell ISE toolbar, click **View** in the menu bar, and click **Show Script Pane Maximized  Ctrl-3**.
1. Use the slider in the lower-right corner of the window to adjust the font size.
1. On line 1, type ```Get-Process``` in the editor window and press the **Run Script** button in the toolbar.
1. This wil display a process listing.
1. Close the Editor by clicking **File** in the menu bar, and **Exit**.
1. Do not save the file.


## Task: PowerShell version
1. Open PowerShell.
1. Run this command: ```$host```
1. This command displays information that represents the current host program. In this case PowerShell.exe. Notice the **Version**.
1. Run this command: ```Get-Host```
1. This is another way of display the previous information.


## Task: Get-Command
1. Run this command: ```Get-Command```
1. This lists all available PowerShell commands on this system.
1. Several things should stand out:
  - Allmost all PowerShell commands should be formed with a well-known verb, followed by a dash (-), followed by a noun. Like this: Stop-Process, Start-Service, Move-Item.
  - Commands have a source. They are organized into folders to keep things manageable.
  - The CommandType exists mostly of cmdlets and functions.
  - In a later chapter we'll go further into this listing.
1. Run this command: ```Get-Command *process*```
1. This lists all available PowerShell commands on this system that contain the word **process**.
1. Run this command: ```Get-Command -Verb Stop```
1. This lists all available PowerShell commands on this system that have a verb of **Stop**, for example Stop-Process and Stop-Service.
1. Run this command: ```Get-Verb```
1. This lists all recommended verbs for PowerShell. In other words: all commands **should** start with one of these verbs.
1. Run this command: ```Get-Command -Noun Process```
1. This lists all commands in PowerShell that have a process noun. In other words: all commands end with **Process**.
1. In a later exercise we're going to explore further on the command listing.


## Task: Get-Help
1. Run this command: ```Get-Command -Noun Help```
1. Notice the Update-Help command. If required, you can run the Update-Help command to retrieve the most current helpfiles from Microsoft over the internet.
1. Run this command: ```Get-Help```
1. This displays a brief help description. **If PowerShell mentions that Help should be updated, confirm this with 'Y'. You can update the help at any other moment with the Update-Help command.**
1. Run this command: ```Get-Help Get-Process```
1. This displays the help about the Get-Process command. Notice the remarks on the bottom of the output.
1. Use the up arrow on your keyboard to retrieve the last command. Append it so it looks like this: ```Get-Help Get-Process -Examples```
1. This command shows examples about running the Get-Process command. The PowerShell authors have put a lot of effort in providing many good and real-world examples for most commands.
1. Run this command: ```Help Get-Process```
1. Notice you're running Help, without the 'Get-' in front of it. The help command is similar to the Get-Help command. Compared to Get-Help, it shows help one screen at a time.
1. Use Enter, spacebar or Q to scroll through the help until the prompt returns.
1. Run this command: ```Get-Help about*```
1. This displays a list of all about-articles in PowerShell. These articles can explain different techniques, without specifically adressing a particular command.
1. Run this command: ```Get-Help about_Variables```
1. This displays help about using variables.
1. Note: You're not required to read this article at this moment. Variables are discussed in another chapter.

# If time permits

## Task: help with a GUI (Graphical User Interface)
1. Run this command: ```Get-Help Get-Process -ShowWindow```
1. This command shows help in a graphical pop-up. Close the pop-up by clicking the X in the upper right corner.
1. Run this command: ```Get-Help Get-Process -online```
1. This command opens a webbrowser that displays the help about the command.
1. Run this command: ```Show-Command Get-Process```
1. Show-Command is helpfull in using commands. It's a graphical window that can help with filling in parameters for a specific command.
1. In the Name field (NOT ComputerName), fill in csrss and click Run.
1. Notice the command is pasted in the PowerShell window. Hit Enter to actually run the command.


## Task: Inspecting Aliases
1. Run this command: ```Get-Alias```
1. This displays a listing of all aliases on the system.
1. Run this command: ```Get-Alias dir, cls, copy```
1. This displays aliases for several popular commands that exist in MS-DOS or the classic Command Prompt (cmd.exe).
1. Run this command: ```Get-Alias ls, clear, cp, ps```
1. This displays aliases for several popular commands that exist in Unix and Linux. Notice that several different aliases can exist for single PowerShell commands. For example: the Clear-Host command has at least two aliases: cls and clear. The Get-ChildItem command has at least three aliases: dir, gci and ls.
1. Run this command: ```Get-Alias gci, gcm, gm, group, sort, select, ft, fl```
1. This displays aliases for several popular PowerShell commands. Many popular commands that exist natively in PowerShell can also be aliased. For example: Get-Process has a gps alias. Get-ChildItem has been aliased as gci.
1. Pay special attention to the last output. These aliases are very common in Powershell. It might even be wise to make a screenshot for future reference.

### Note: it is a best practice to use as few aliases as possible. This way script readability is increased. Aliases exist primarily to speed up entering command's in the shell. You're not supposed to use aliases in a scriptfile.


## Task: Creating Aliases
1. Run this command: ```New-Alias edit notepad```
1. You now created an alias for the notepad application.
1. Run this command: ```edit```
1. This will start notepad, since that's what the alias is referring to.
1. Close notepad to return to PowerShell.
1. Run this command to close PowerShell: ```exit``` 
1. Now start PowerShell again.
1. Run this command: ```edit```
1. You'll receive an error that this term is not recognized. That's because aliases only exist in memory. In a later exercise we'll learn how to create aliases in a PowerShell profile and 'make it stick'.
1. Keep the PowerShell console running for the next task.


# History lessons in PowerShell
A famous saying goes like this: **"those who don't know history are destined to repeat it"**. You don't want to keep typing the same commands over and over again, do you? So here are some history lessons.

## Task: History
1. Open a PowerShell console.
1. Run this command: ```Get-Service```
1. Run this command: ```Get-ChildItem```
1. Run this command: ```Get-Process```
1. Now that we have some commands in our session history, let's investigate it.
1. Run this command: ```Get-Command -Noun History```
1. This lists all commands that handle the PowerShell history.
1. Run this command: ```Get-History```
1. This should list at least the last four commands.
1. Take notice of the number that references the Get-Process command that's lowest in the list.
1. Invoke that command from history using the following command (replace 999 with the number you found in the previous step):
1. ```Invoke-History 999```
1. Notice that the Get-Process command is executed.
1. Run this command: ```Clear-History```
1. This has erased the history from memory. Inspect it with this command: ```Get-History```
1. Run this command: ```Get-ChildItem```
1. Now we have some fresh commands in the console history. Inspect it with this command: ```Get-History```
1. Run this command to close PowerShell: ```exit```
