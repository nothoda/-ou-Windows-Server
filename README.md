Import-Module ActiveDirectory
$parentPath = "DC=egtrust,DC=local"
$ouNames = @("HR", "IT", "SEALS")
foreach ($ouName in $ouNames) {
    if (-not (Get-ADOrganizationalUnit -Filter { Name -eq $ouName } -SearchBase $parentPath -ErrorAction SilentlyContinue)) {
        New-ADOrganizationalUnit -Name $ouName -Path $parentPath
        Write-Host "Created OU: $ouName"
    } else {
        Write-Host "OU already exists: $ouName"
    }
}
