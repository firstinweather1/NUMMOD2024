WRF Notes
ssh rshroff@derecho.hpc.ucar.edu (logs you into derecho supercomputer)
Site to download data: https://www2.mmm.ucar.edu/wrf/users/download/free_data.html
WRF tutorial link: https://www2.mmm.ucar.edu/wrf/OnLineTutorial/CASES/SingleDomain/wrf.php
WRF users page: https://www2.mmm.ucar.edu/wrf/users/forecasts.html
Useful Commands: 
pwd (shows your current path)
ls -ltr (shows errors and all files)
ls *.exe (allows you to see all exe files in directory)
nano error file (shows what is wrong or errors in rsl.out.0000)
mv: rename a file
rm:  delete a file, rm * (deletes all files with certain file name)
ncdump file_name | more (allows you to see contents of file)
Important to Note: 
•	interval_seconds = model timestep (3600 = 1 hour)
•	time_step = internal model timestep (10 = 10 seconds, lower numbers needed for higher resolution to prevent WRF from crashing)
Login Node Methodology: 
To download GFS data…
1.	Go to provided website above and download generated csh script
2.	scp csh script into data directory (must do this in local terminal)
3.	make csh script an executable (chmod +x file_name.csh)
4.	Run file and then delete csh script for clarity
After you have finished downloading your data into your data directory go into your wps4.1v directory…
1.	ln -sf ungrib/Variable_Tables/Vtable.GFS Vtable
2.	./link_grib.csh ../DATA/matthew/fnl (beginning of file name)
3.	Edit namelist.wps by using nano namelist.wps
4.	Run ungrib (./ungrib.exe)
5.	Edit namelist.wps (to enter, do nano namelist.wps)
6.	Run geogrid (./geogrid.exe)
7.	Run metgrid (./metgrid.exe)
Now go into the WRF directory…

1.	Switch into test/em_real directory
2.	Link met_em files created with metgrid.exe (ln -sf ../../../wpsv4.1/met_em.d01.2016-10* .)
3.	Edit namelist.input
4.	Run real.exe (./real.exe)
5.	Run wrf.exe (./wrf.exe)
6.	Copy wrfout files into directory (bypasses colon issue)
To copy data from Derecho to local machine (must be in local terminal)…
scp -r rshroff@derecho.hpc.ucar.edu:/glade/u/home/rshroff/wrfv4.1/test/em_real/January2016data . 
scp -r rshroff@derecho.hpc.ucar.edu:/glade/derecho/scratch/rshroff/wrfv4.1/test/em_real/January2016data . 
To copy data from local machine to derecho (must be in local terminal)…
scp -r /Users/shrof/Downloads/filename.csh rshroff@derecho.hpc.ucar.edu:/glade/u/home/rshroff/SpringNumMod/arctic
Note: 
If you’re running a WRF simulation that is excessively large, running real.exe will in the login node will cause your run to crash. Accordingly, for simulations with large compute requirements, runs must be submitted to the working directory. To do so, you can run an executable script in the log in node that then runs real.exe in the working directory instead of the log in node. 
Working Node Methodology: 
To run high resolution simulations, you must work in working directory: 
After you have finished downloading your data into your data directory go into your wps4.1v directory…
1.	ln -sf ungrib/Variable_Tables/Vtable.GFS Vtable
2.	./link_grib.csh /glade/derecho/scratch/rshroff/wrf_folder/SpringNumMod/arctic/gfs (beginning of file name)
3.	Edit namelist.wps by using nano namelist.wps
4.	Run ungrib (./ungrib.exe)
5.	Edit namelist.wps (to enter, do nano namelist.wps)
6.	Run geogrid (./geogrid.exe)
7.	Run metgrid (./metgrid.exe)
Now go into the WRF directory…

1.	Switch into test/em_real directory
2.	Link met_em files created with metgrid.exe (ln -sf ../../../wpsv4.1/met_em.d01.2016-10* .)
3.	Edit namelist.input
4.	Run real.exe (./real.exe) using qcmd -A UCOR0073 -- ./real.exe (shortcut to submit job, gives you one node), if job is very big run runreal.csh script
5.	Run wrf.exe (./wrf.exe) using qsub runwrf.csh (32 cores instead of 1, prevents crashing)
6.	Copy wrfout files into directory (bypasses colon issue)

Editing Domain: 
•	To edit resolution, adjust dx and dy (dx, dy = 2700 = 2.7 km resolution)
•	Ref_lat and ref_lon determines center of domain
•	E_we and e_sn determines the domain size because this is the number of grid points (so if resolution is increased your domain will automatically decrease in size)
•	To increase domain, use formula (e_we = domain length (meters) / dx)
File Name: 
•	To edit file name, go to test/em_real directory and open namelist.output file using nano

Nested Domains: 
•	Better approach is to use nested domain when running high resolution simulations
•	When doing nested domain, you want each successive domain to be about 1/3 of the previous domain, so if your first domain is 12 km, the next one should be 4 km, and …



