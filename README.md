
# Search-Registry

This PowerShell module makes searching registry keys easy.  See usage below.

**Source:** [https://gallery.technet.microsoft.com/scriptcenter/Search-Registry-Find-Keys-b4ce08b4](https://gallery.technet.microsoft.com/scriptcenter/Search-Registry-Find-Keys-b4ce08b4)


# Install with a one-line command
Run **PowerShell** as **Administrator**, paste this (one line): 

    if(-not (Test-Path "C:\Windows\System32\WindowsPowerShell\v1.0\Modules\Search-Registry")) { New-Item -Type Directory -Name "Search-Registry" -Path "C:\Windows\System32\WindowsPowerShell\v1.0\Modules"; (New-Object System.Net.WebClient).DownloadFile("https://raw.githubusercontent.com/asheroto/Search-Registry/master/Search-Registry.psm1", "C:\Windows\System32\WindowsPowerShell\v1.0\Modules\Search-Registry\Search-Registry.psm1") }
then press enter

**This command does the following:**

 - Checks for a Search-Registry module folder in `C:\Windows\System32\WindowsPowerShell\v1.0\Modules`
 - If the folder doesn't exist
	 - Create the folder
	 - Download **Search-Registry.psm1** and place it in the folder

# Install error "could not create SSL/TLS secure channel"
Run **PowerShell** as **Administrator**, paste this:

    [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12

then press enter, then re-run the command you were attempting

# Install manually

 1. Go here: `C:\Windows\System32\WindowsPowerShell\v1.0\Modules`
 2. Create a new folder called `Search-Registry`
 3. Open Notepad
 4. Copy and paste the contents of `Search-Registry.psm1` from GitHub Raw
 5. Save the file as `C:\Windows\System32\WindowsPowerShell\v1.0\Modules\Search-Registry\Search-Registry.psm1`

# Usage Examples
**Search key names, value names, and value data:**

    Search-Registry -Path HKLM:\SOFTWARE -Recurse -SearchRegex "cisco|anyconnect"
    
Tip: to see the entire string append `| fl` to the command

**Search only key names and value names**

    Search-Registry -Path HKLM:\SOFTWARE -Recurse -SearchRegex "cisco|anyconnect" -KeyName -ValueName

**Search for different key names and value names:**

    Search-Registry -Path HKLM:\SOFTWARE -Recurse -KeyNameRegex "^cisco$|^anyconnect$" -ValueNameRegex "cisco|anyconnect"

# Get-Help Search-Registry
**NAME**

Search-Registry

**SYNOPSIS**

Searches registry key names, value names, and value data (limited).

**SYNTAX**

    Search-Registry [-Path] <String[]> [-Recurse] -SearchRegex <String> [-KeyName] [-ValueName] [-ValueData] [<CommonParameters>]

    Search-Registry [-Path] <String[]> [-Recurse] [-KeyNameRegex <String>] [-ValueNameRegex <String>] [-ValueDataRegex <String>] [<CommonParameters>]


**DESCRIPTION**

This function can search registry key names, value names, and value data (in a limited fashion). It outputs custom objects that contain the key and the first match type (KeyName, ValueName, or ValueData).

**PARAMETERS**

    -Path <String[]>
        Registry path to search
    
    -Recurse [<SwitchParameter>]
        Specifies whether or not all subkeys should also be searched
    
    -SearchRegex <String>
        A regular expression that will be checked against key names, value names, and value data (depending on the
        specified switches)
    
    -KeyName [<SwitchParameter>]
        When the -SearchRegex parameter is used, this switch means that key names will be tested (if none of the three
        switches are used, keys will be tested)
    
    -ValueName [<SwitchParameter>]
        When the -SearchRegex parameter is used, this switch means that the value names will be tested (if none of the
        three switches are used, value names will be tested)
    
    -ValueData [<SwitchParameter>]
        When the -SearchRegex parameter is used, this switch means that the value data will be tested (if none of the
        three switches are used, value data will be tested)
    
    -KeyNameRegex <String>
        Specifies a regex that will be checked against key names only
    
    -ValueNameRegex <String>
        Specifies a regex that will be checked against value names only
    
    -ValueDataRegex <String>
        Specifies a regex that will be checked against value data only
    
    <CommonParameters>
        This cmdlet supports the common parameters: Verbose, Debug,
        ErrorAction, ErrorVariable, WarningAction, WarningVariable,
        OutBuffer, PipelineVariable, and OutVariable. For more information, see
        about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

