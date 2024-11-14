# savepshistory
It has always bugged me that there was not quick way to save the PowerShell history so this is a small function to be able to do that.

To implement this.

Find the location of your powershell profile and edit the profile file.

You can do this by entering $PROFILE at the PowerShell command prompt

edit this file ie. notepad <profile>

Add this function to the profile file and save:

```
function Save-PSHistory {
    param (
        [Parameter(Mandatory=$true)]
        [string]$OutputPath
    )

    try {
        $historyPath = (Get-PSReadlineOption).HistorySavePath
        Copy-Item -Path $historyPath -Destination $OutputPath -ErrorAction Stop
        Write-Host "History saved to $OutputPath" -ForegroundColor Green
    }
    catch {
        Write-Host "Error: $_" -ForegroundColor Red
    }
}

```

Re-initialize the profile:

```
. $PROFILE
```

and to save the the historyou can simpply enter:

```
Save-PSHistory <filename and/or directory path>
```

