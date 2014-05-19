# Author: Brian Pedigo   
#
# Date: May 2014 
#
# File name: 
#    .----------------.  .----------------.  .----------------.  .----------------.  .----------------.  .----------------. 
#| .--------------. || .--------------. || .--------------. || .--------------. || .--------------. || .--------------. |
#| |  _________   | || |     _____    | || |  _______     | || |     ______   | || | ____    ____ | || |  ________    | |
#| | |  _   _  |  | || |    |_   _|   | || | |_   __ \    | || |   .' ___  |  | || ||_   \  /   _|| || | |_   ___ `.  | |
#| | |_/ | | \_|  | || |      | |     | || |   | |__) |   | || |  / .'   \_|  | || |  |   \/   |  | || |   | |   `. \ | |
#| |     | |      | || |      | |     | || |   |  __ /    | || |  | |         | || |  | |\  /| |  | || |   | |    | | | |
#| |    _| |_     | || |     _| |_    | || |  _| |  \ \_  | || |  \ `.___.'\  | || | _| |_\/_| |_ | || |  _| |___.' / | |
#| |   |_____|    | || |    |_____|   | || | |____| |___| | || |   `._____.'  | || ||_____||_____|| || | |________.'  | |
#| |              | || |              | || |              | || |              | || |              | || |              | |
#| '--------------' || '--------------' || '--------------' || '--------------' || '--------------' || '--------------' |
# '----------------'  '----------------'  '----------------'  '----------------'  '----------------'  '----------------' 
#
# Purpose: to make changing directorys, opening directorys, finding files,and opening programs simple



# this function is used to set up the files that will store the short cut data
function check-setup () {

    $directoryBasePath = "$([Environment]::GetFolderPath('LocalApplicationData'))\tricmd"
    $script:directoryPath1 = $directoryBasePath + "\goto.txt"
    $script:directoryPath2 = $directoryBasePath + "\open.txt"

    $hasdir = Test-Path $directoryBasePath
    $hasfile1 = Test-Path $directoryPath1
    $hasfile2 = Test-Path $directoryPath2

    if(!$hasdir)
    {
        new-item -itemtype directory -path $directoryBasePath
        new-item $directoryPath1 -type file
        new-item $directoryPath2 -type file
    }
    else
    {
   
        if(!$hasfile1) {  new-item $directoryPath1 -type file }
        if(!$hasfile2) {  new-item $directoryPath2 -type file }
    }

}


check-setup


#┌─┐┬┬─┐┌─┐┌┬┐  ┌─┐┌┬┐┌┬┐
#├┤ │├┬┘└─┐ │   │  │││ ││
#└  ┴┴└─└─┘ ┴   └─┘┴ ┴─┴┘
################################
function bir{                  #
                               #
################################
    function counter
    {
        BEGIN   { $x = 0 }
        PROCESS { $x += 1 }
        END     { $x }
    }
###############################################################################
function display {
$total = dir $dir | counter
write-host "`n"
write-host "==============================================================="

write-host "total number of files in pwd" $total

write-host "total number of folders in pwd" $folders -foregroundcolor green

if($exe -gt 0){
write-host "total number of exe files" $exe -foregroundcolor Yellow
}

if($cmd -gt 0){
write-host "total number of bat files" $cmd -foregroundcolor red
}

if($py -gt 0){
write-host "total number of py files" $py -foregroundcolor red
}

if($vbs -gt 0){
write-host "total number of vbs files" $vbs -foregroundcolor magenta
}

if($ps1 -gt 0 ){
write-host "total number of ps1 files" $ps1 -foregroundcolor blue
}
if($cpp -gt 0){
write-host "total number of cpp files" $cpp -foregroundcolor cyan
}
}        
###########################################################################




function high_light
{
param ($dir = ".", $all = $false) 
$script:exe = 0
$script:cmd = 0 
$script:py = 0
$script:vbs = 0
$script:ps1 = 0
$script:cpp = 0
$script:folders = 0




$origFg = $host.ui.rawui.foregroundColor 
if ( $all ) { $toList = ls -force $dir }

    else { $toList = ls $dir }

 

    foreach ($Item in $toList)  

    { 

        Switch ($Item.Extension)  

        { 

            ".Exe" {$host.ui.rawui.foregroundColor = "Yellow" ; $script:exe++ } #1

            ".bat" {$host.ui.rawui.foregroundColor = "Red"; $script:cmd++ } #2

            ".py" {$host.ui.rawui.foregroundColor = "Red"; $script:py++} #3

            ".vbs" {$host.ui.rawui.foregroundColor = "Magenta"; $script:vbs++ } #4
            
            ".ps1" {$host.ui.rawui.foregroundColor = "Blue"; $script:ps1++ } #5
            
            ".cpp" {$host.ui.rawui.foregroundColor = "Cyan"; $script:cpp++} #6

            Default {$host.ui.rawui.foregroundColor = $origFg} 

        } 

        if ($item.Mode.StartsWith("d")) {$host.ui.rawui.foregroundColor = "Green"; $script:folders++} #7

        $item 
        
       }  

    $host.ui.rawui.foregroundColor = $origFg 

}
#############################################################################################

#----Main--------------------------------------#
high_light
display
}

#┌─┐┌─┐┌─┐┌─┐┌┐┌┌┬┐  ┌─┐┌┬┐┌┬┐
#└─┐├┤ │  │ ││││ ││  │  │││ ││
#└─┘└─┘└─┘└─┘┘└┘─┴┘  └─┘┴ ┴─┴┘
####################################################################################################################################################################
function open ([string]$label, [string]$Opath, [switch]$add, [switch]$a, [switch]$showall,[switch]$sa,[switch]$clear, [switch]$delete, [switch]$help, [switch]$h){ #
                                                                                                                                                                   #
####################################################################################################################################################################
function dup-check($dircontent){

foreach($item in $dircontent)
         {
          
          $keys = $item.split('|')
          
           if($keys[0] -eq $label.ToLower())
            {
              return $true;
   
            }
         }
 return $false
}
###############################################

function open-label($labels)
{
        $filecontect = Get-Content $directoryPath2
        
        foreach($item in $filecontect)
            {
               $key = $item.split("|")
               
               if($key[0] -eq $labels)
               {
                    start $key[1]
                    return
               }   
            }
     write-host "Label not found!"
}

##############################################

function show-all()
{
        $filecontect = Get-Content $directoryPath2
        
        if($filecontect -eq $null)
        {
        
        write-host "no information to show!"
        
        
        }
        else{
        
        write-host "label                       program"
        write-host "-----------------------------------"
        foreach($item in $filecontect)
            {
               $key = $item.split("|")
               $padding = 30 - $key[0].count 
               
               write-host $key[0].Padright($padding, " ")  $key[1]
                
            }  
          }     
}

###############################################

function clear-file($labels)
{
        $filecontect = Get-Content $directoryPath2
        
        foreach($item in $filecontect)
            {
               $key = $item.split("|")
               
               if($key[0] -eq $labels)
               {
                    $delete = $item
                    break
               }   
            }
            
         if($delete -ne "")
           {
                    $filecontect = $filecontect |? {$_ -ne $delete}

                    Clear-Content $directoryPath2
                
                    Add-Content -Value $filecontect -Path $directoryPath2
                    return
           }
         
         
     write-host "Label not found!"

}

#########################################################################

function helper{
    
        Write-Host "`n"
        Write-Host "Open Directory Help"
        Write-Host "-----------------"
        Write-Host "Usage:"
        Write-Host "    open label"
        Write-Host "    open label -delete or -d"
        Write-Host "    open label -show or -s"
        Write-Host "    open label -add or -a"
        Write-Host "    open -showAll or -sa"
        Write-Host "    open -clear or -c"
        Write-Host "`n"
        Write-Host "Switches:"
        Write-Host "    -add or -a             Adds the current directory."
        Write-Host "    -delete or -d          Remove the given key from the directory."
        Write-Host "    -showAll or -sa        Show all the keys and values in the directory."
        Write-Host "    -show or -s            Show the specific key and value."
        Write-Host "    -clear or -c           Clears all the keys and values in the directory."
        Write-Host "    -help or -h            Displays this screen."
        Write-Host "`n"
    
        return
}




#------------------Main-----------------------------------------------#

if($add -or $a)
{
    
    
    if($label -and $Opath)
    {
         $dircontent = Get-Content $directoryPath2
         
         if($dircontent -eq $null)
         {
          $isDup = $false
         }
         else{
         $isDup = dup-check($dircontent)
         }
         
          if(!$isDup)
          {  
            $compkey = $label.toLower() + "|" + $Opath
            add-content -value $compkey -path $directoryPath2
          }
          else
          {
          write-host " Duplicate label was used"
          }
         
    } 
    elseif($label.count -eq 0 -or $Opath.count -eq 0)
    {
    write-host "you need both a label and a file to open"
    return
    }    
    
  return  
}

if($label -and !$delete)
    {
    open-label($label)
    }

if($showall -or $sa)
    {
        show-all
        return
    }
if($delete)
   {
   clear-file($label)
   }
   

if($clear -or $c)
    {
        $response = Read-Host "Are you sure you want to clear? [Y] or [N]"

        

        if($response -eq "y")
        {
            Clear-Content $directoryPath2
        }

        return
    }

if($help -or $h)
    {
    helper
    }         

}

#┌┬┐┬ ┬┬┬─┐┌┬┐  ┌─┐┌┬┐┌┬┐
# │ ├─┤│├┬┘ ││  │  │││ ││
# ┴ ┴ ┴┴┴└──┴┘  └─┘┴ ┴─┴┘
###############################################################################################################################################################################################################################################
function goto([string]$key, [string]$selectedPath = "",[switch]$ii, [switch]$help, [switch]$h, [switch]$add, [switch]$a, [switch]$delete, [switch]$d, [switch]$clear, [switch]$c, [switch]$show, [switch]$s, [switch]$showAll, [switch]$sa )  #
                                                                                                                                                                                                                                              #                   
###############################################################################################################################################################################################################################################
{
    #------------------------------------Help------------------------------------
    if($help -or $h)
    {
        Write-Host
        Write-Host "Go Directory Help"
        Write-Host "-----------------"
        Write-Host "Usage:"
        Write-Host "    goto label"
        Write-Host "    goto label -delete or -d"
        Write-Host "    goto label -show or -s"
        Write-Host "    goto label -add or -a"
        Write-Host "    goto label C:\SomePath -add or -a"
        Write-Host "    goto -showAll or -sa"
        Write-Host "    goto -clear or -c"
        Write-Host
        Write-Host "Switches:"
        Write-Host "    -add or -a             Adds the current directory."
        Write-Host "    -delete or -d          Remove the given key from the directory."
        Write-Host "    -showAll or -sa        Show all the keys and values in the directory."
        Write-Host "    -show or -s            Show the specific key and value."
        Write-Host "    -clear or -c           Clears all the keys and values in the directory."
        Write-Host "    -help or -h            Displays this screen."
        Write-Host
   
        return
    }
    
    #------------------------------------Show all keys------------------------------------
    if($showAll -or $sa)
    {
        $directoryContent = Get-Content $directoryPath1

        if($directoryContent)
        {
            $longestCount = 0
            $directoryArray = @{}

            foreach($item in $directoryContent)
            {
                $keys = $item.Split("|")
                $keyLength = $keys[0].Length

                if($longestCount -eq 0)
                {
                    $longestCount = $keyLength
                }
            
                if($keyLength -gt $longestCount)
                {
                    $longestCount = $keyLength
                }
            }

            if($longestCount -gt 0)
            {
                $lineBreak = ""
                $dashLine = ""

                for($index = 0; $index-lt $longestCount; $index++)
                {
                    $lineBreak += " ";
                    $dashLine += "-"
                }

                Write-Host
                Write-Host "Key" $lineBreak "Value"
                Write-Host $dashLine "    ------------------" -ForegroundColor Yellow

                foreach($item in $directoryContent)
                {
                    $keys = $item.Split("|")
                    $subCount = $longestCount - $keys[0].Length
                    $middleBreak = "   "

                    for($index = 0; $index -lt $subCount; $index++)
                    {
                        $middleBreak += " "
                    }   
                
                    Write-Host $keys[0] $middleBreak $keys[1]
                }

                Write-Host
            }
        }
    }

    #------------------------------------Show key------------------------------------
    if($show -or $s)
    {
        if($key)
        {
            $directoryContent = Get-Content $directoryPath1

            if($directoryContent)
            {
                $specificValue = @{}

                foreach($item in $directoryContent)
                {
                    $keys = $item.Split("|")

                    if($keys[0] -eq $key.ToLower())
                    {
                        $specificValue = $keys

                        break
                    }
                }

                if($specificValue.Count -ne 0)
                {
                    $dashLine = ""
                    $lineBreak = ""

                    for($index = 0; $index-lt $specificValue[0].Length; $index++)
                    {
                        $lineBreak += " ";
                        $dashLine += "-"
                    }

                    Write-Host
                    Write-Host "Key" $lineBreak "Value"
                    Write-Host $dashLine "    ------------------" -ForegroundColor Yellow
                    Write-Host $specificValue[0] "    " $specificValue[1]
                    Write-Host
                }
            }
        }

        return
    }

    #------------------------------------Clear all keys------------------------------------
    if($clear -or $c)
    {
        $response = Read-Host "Are you sure you want to clear? [Y] or [N]"

        Write-Host $val

        if($response -and $response.ToLower() -eq "y")
        {
            Clear-Content $directoryPath1
        }

        return
    }

    #------------------------------------Delete Key------------------------------------
    if($delete -or $d)
    {
        if($key)
        {
            $directoryContent = Get-Content $directoryPath1

            if($directoryContent)
            {
                $keyToDelete = ""

                foreach($item in $directoryContent)
                {
                    $keys = $item.Split("|")

                    if($keys[0] -eq $key.ToLower())
                    {
                        $keyToDelete = $item

                        break
                    }
                }

                if($keyToDelete -ne "")
                {
                    $directoryContent = $directoryContent |? {$_ -ne $keyToDelete}

                    Clear-Content $directoryPath
                
                    Add-Content -Value $directoryContent -Path $directoryPath1
                }
            }
        }

        return
    }

    #------------------------------------Add key------------------------------------

    if($add -or $a)
    {
        if($key)
        {
            $directoryContent = Get-Content $directoryPath1
            $isDuplicate = $false
        
            if($directoryPath)
            {
                foreach($item in $directoryContent)
                {
                    $keys = $item.Split('|')

                    if($keys[0] -eq $key.ToLower())
                    {
                        $isDuplicate = $true;

                        break;
                    }
                }
            }

            if(!$isDuplicate)
            {
                $compositeKey = $key.ToLower() + "|"

                if($selectedPath)
                {
                    $compositeKey += $selectedPath
                }
                else
                {
                    $compositeKey += $pwd
                }

                Add-Content -value $compositeKey -Path $directoryPath1
            }
        }

        return
    }

    #------------------------------------Push key With Bir------------------------------------
    if($key)
    {
        $directoryContent = Get-Content $directoryPath1
        $bookmark = ""

        if($directoryContent)
        {
            foreach($item in $directoryContent)
            {
                $keys = $item.Split("|")

                if($keys[0] -eq $key.ToLower())
                {
                    $bookmark = $keys[1]

                    break
                }
            }

            if($bookmark)
            {
               
                Push-Location $bookmark
                bir
            }
        }
    }

#------------------------------------Push key With Invoke------------------------------------
    if($key -and $ii)
    {
        $directoryContent = Get-Content $directoryPath1
        $bookmark = ""

        if($directoryContent)
        {
            foreach($item in $directoryContent)
            {
                $keys = $item.Split("|")

                if($keys[0] -eq $key.ToLower())
                {
                    $bookmark = $keys[1]

                    break
                }
            }
  
            if($bookmark)
            {
                
                Push-Location $bookmark
                ii .
            }
        }
    }
}





