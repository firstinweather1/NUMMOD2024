# NUMMOD2024
Stores code for numerical modeling class during spring 2024. 

Steps to Run WRF on terminal: 

Log into Derecho super computer

>> ssh -X -Y <username>@derecho.hpc.ucar.edu

# (password, duo authorization)

# Upon doing this, you should be in: 

# /glade/u/home/$user ($ is the variable, spits out the contents of the variable)

# For funzies: 

>> echo $USER (should get your name)

Somewhere on file tree: 

>> cd /glade/work/wrfhelp/derecho_pre_compiled_code

>> cp -rp wrfv4.1 ~/
>> cp -rp wpsv4.1 ~/

cd ~/ takes you back to the original directory 


# In tutorial: Downloads matthew data to your computer. Go to your downloads folder on your personal computer. Eventually we will use wget here to get our data. 

downloads>> 
scp -r /Users/gabriellarouche/downloads/matthew_1deg.tar glarouche@derecho.hpc.ucar.edu:/glade/u/home/glarouche/EAS5555/DATA
scp -r /Users/shrof/Downloads/matthew_1deg/matthew rshroff@derecho.hpc.ucar.edu:/glade/u/home/rshroff/SpringNumMod (DO THIS IN THE HOME TERMINAL)
scp -r "C:\Users\Henning Schade\Downloads\matthew_1deg.tar.gz" hschade@derecho.hpc.ucar.edu:/glade/u/home/hschade/DATA
Now, in your data: tar -xf matthew_1deg.tar.gz

After you have finished downloading your data into your data directory go into your wps4.1v directory…

ln -sf ungrib/Variable_Tables/Vtable.GFS Vtable
./link_grib.csh ../DATA/matthew/fnl ***last step Henning did***
Edit namelist.wps by using nano namelist.wps
Run ungrib (./ungrib.exe)
Edit namelist.wps (to enter, do nano namelist.wps)
Run geogrid (./geogrid.exe)
Run metgrid (./metgrid.exe)
Now go into the WRF directory…

Switch into test/em_real directory
Link met_em files created with metgrid.exe (ln -sf ../../../WPS/met_em.d01.2016-10* .)
Edit namelist.input
Run real.exe (./real.exe)
Run wrf.exe (./wrf.exe)


