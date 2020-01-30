![MIKES DATA WORK GIT REPO](https://raw.githubusercontent.com/mikesdatawork/images/master/git_mikes_data_work_banner_01.png "Mikes Data Work")        

# Get Number Of Cores In SQL Server
**Post Date:  October 18, 2016**        



## Contents    
- [About Process](##About-Process)  
- [SQL Logic](#SQL-Logic)  
- [Build Info](#Build-Info)  
- [Author](#Author)  
- [License](#License)       

## About-Process

<p>From time to time you'll need to visit your license costs, and to do so you'll need to run some queries against sys.dm_os_sys_info so you can get the number of cores for SQL Server.
  
If you want all the dirt on sys.dm_os_sys_info just go here: https://msdn.microsoft.com/en-us/library/ms175048(v=sql.110).aspx
Here's some quick SQL Logic to get you started.</p>

![Get Number Of Cores In SQL Server](https://mikesdatawork.files.wordpress.com/2016/10/image0013.png "Get Number of Cores In SQL Server")
 

    
## SQL-Logic
```SQL
use master;
set nocount on
select
     'physical_cpu' = cpu_count / hyperthread_ratio
,    'cores' =
         case
            when hyperthread_ratio = cpu_count then cpu_count
            else (cpu_count / hyperthread_ratio) * ((cpu_count - hyperthread_ratio) / (cpu_count / hyperthread_ratio))
         end
,     'logical_cpu' =
          case
             when hyperthread_ratio = cpu_count then cpu_count
          else ((cpu_count - hyperthread_ratio) / (cpu_count / hyperthread_ratio))
       end
from
master.sys.dm_os_sys_info


```
Of course; if you're curious about the logic, and need a simple way to verify you can always get a quick glance from basically using performance monitor. Just right-click the task-bar, and click 'Task Manager'. If you look at the lower right you'll see the number of cores and the number of logical processors.

![Check Cores]( https://mikesdatawork.files.wordpress.com/2016/10/image0021.png "Check Cores")
 


[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

[![Gist](https://img.shields.io/badge/Gist-MikesDataWork-<COLOR>.svg)](https://gist.github.com/mikesdatawork)
[![Twitter](https://img.shields.io/badge/Twitter-MikesDataWork-<COLOR>.svg)](https://twitter.com/mikesdatawork)
[![Wordpress](https://img.shields.io/badge/Wordpress-MikesDataWork-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

 
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Mikes Data Work](https://raw.githubusercontent.com/mikesdatawork/images/master/git_mikes_data_work_banner_02.png "Mikes Data Work")

