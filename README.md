# Clean-PC-s-Junk-File-By-Script
Clean PC's Junk File By Script

1. Open Windows PowerShell ISE (x86)
2.  Create New Script and paste the following code

-----------------------------------------------------------

	$objShell = New-Object -ComObject Shell.Application
	$objFolder = $objShell.Namespace(0xA)
	$WinTemp = "c:\Windows\Temp\*"
	
#1#	Empty Recycle Bin #
	write-Host "Emptying Recycle Bin." -ForegroundColor Cyan 
	$objFolder.items() | %{ remove-item $_.path -Recurse -Confirm:$false}
	
#2# Remove Temp
	write-Host "Removing Temp" -ForegroundColor Green
    Set-Location “C:\Windows\Temp”
	Remove-Item * -Recurse -Force -ErrorAction SilentlyContinue

    Set-Location “C:\Windows\Prefetch”
    Remove-Item * -Recurse -Force -ErrorAction SilentlyContinue

    Set-Location “C:\Documents and Settings”
    Remove-Item “.\*\Local Settings\temp\*” -Recurse -Force -ErrorAction SilentlyContinue

    Set-Location “C:\Users”
    Remove-Item “.\*\Appdata\Local\Temp\*” -Recurse -Force -ErrorAction SilentlyContinue
	
#3# Running Disk Clean up Tool 
	write-Host "Finally now , Running Windows disk Clean up Tool" -ForegroundColor Cyan
	cleanmgr /sagerun:1 | out-Null 
	
	$([char]7)
	Sleep 3
	write-Host "I finished the cleanup task,Bye Bye " -ForegroundColor Yellow 
	Sleep 3
##### End of the Script ##### 


--------------------------------------

3. Save the code with CleanPc.sp1
4. Run it with Powershell
5. Done
