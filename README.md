# Register-SchedularTask-Loop

$servers = @("Server1")

foreach($server in $servers){

<# Invoke Command will alow us to execute and target the servers in our loop using sciptblock #> 
Invoke-Command -ComputerName $server -ScriptBlock{


<# Creating our Variables for Action and Trigger which are essential for a scheduling a task #> 
$scriptpath = "\\REMOTE\SCRIPT\LOCATION\Script.ps1"

<# -Argument is a great way of selecting the remove script location #> 
$action = New-ScheduledTaskAction -Execute "Powershell.exe" -Argument "-file $scriptpath" 
$trigger = New-ScheduledTaskTrigger -DaysInterval 14 -At 8:00AM

<# Note you dont have to put password, if you use user name it will prompt for password and hash it with the script #> 
Register-ScheduledTask -Action $action -Trigger $trigger -TaskPath "Test Task" -TaskName "Test Task" -Description "Test task" -User "USERNAME" -Password "PASSWORD"

}

}
