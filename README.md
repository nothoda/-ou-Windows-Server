# Define the parent path where the OUs will be created
$parentPath = "DC=egtrust,DC=local"

# Create an array of OU names
$ouNames = @("HR", "IT", "SEALS")

# Loop through each OU name and create it if it doesn't already exist
foreach ($ouName in $ouNames) {
    if (-not (Get-ADOrganizationalUnit -Filter { Name -eq $ouName } -SearchBase $parentPath -ErrorAction SilentlyContinue)) {
        New-ADOrganizationalUnit -Name $ouName -Path $parentPath
        Write-Host "Created OU: $ouName"
    } else {
        Write-Host "OU already exists: $ouName"
    }
}
