If there is an error when running stoped test, it may be due to unsuccesful download of parameter files. You may have to download it manually from the permanent store repository. The following files need to be downloaded:
# URLs for StopET data
stopet_download_urls = {
    "stopet_parameters.nc": "https://figshare.com/ndownloader/files/34923690",
    "monthly_cont_percentage.nc": "https://figshare.com/ndownloader/files/34923684",
    "dpetdt.nc": "https://figshare.com/ndownloader/files/34923663",
    "hpet_slope.nc": "https://figshare.com/ndownloader/files/34923720",
    "meanshift_had.nc": "https://figshare.com/ndownloader/files/49400419",
    "stdshift_had.nc": "https://figshare.com/ndownloader/files/49400425"
}

and copy and paste in the corresponing directory.

By default it should be stored in:
'/home/username/anaconda3/envs/cwld/lib/python3.11/site-packages/cuwalid/stopet/stopet_parameters/meanshift_had.nc'




(cwld) c1755103@aquifer:~$ python -m cuwalid.tests.stopet.run_tests
Warning: The following required data files are missing:
 - dpetdt.nc
 - hpet_slope.nc
 - meanshift_had.nc
 - monthly_cont_percentage.nc
 - stdshift_had.nc
 - stopet_parameters.nc
Please run the following command to download the necessary files:
    python -m cuwalid.tools.download_data
Error: Some necessary parameter files are missing.
Please run the command below to download:
python -m cuwalid.tools.download_data
(cwld) c1755103@aquifer:~$ python -m cuwalid.tools.download_data
Downloading stopet_parameters.nc...
stopet_parameters.nc: 0.00B [00:00, ?B/s]
Downloading monthly_cont_percentage.nc...
monthly_cont_percentage.nc: 0.00B [00:00, ?B/s]
Downloading dpetdt.nc...
dpetdt.nc: 0.00B [00:00, ?B/s]
Downloading hpet_slope.nc...
hpet_slope.nc: 0.00B [00:00, ?B/s]
Downloading meanshift_had.nc...
meanshift_had.nc: 0.00B [00:00, ?B/s]
Downloading stdshift_had.nc...
stdshift_had.nc: 0.00B [00:00, ?B/s]
(cwld) c1755103@aquifer:~$ python -m cuwalid.tests.stopet.run_tests
Execution type is depreciated as both methods are combined now. Please feel free to delete it from the config file.
Traceback (most recent call last):
  File "<frozen runpy>", line 198, in _run_module_as_main
  File "<frozen runpy>", line 88, in _run_code
  File "/home/c1755103/anaconda3/envs/cwld/lib/python3.11/site-packages/cuwalid/tests/stopet/run_tests.py", line 14, in <module>
    run_stoPET(input_file_path)
  File "/home/c1755103/anaconda3/envs/cwld/lib/python3.11/site-packages/cuwalid/stopet/main_stopet.py", line 62, in run_stoPET
    run_stoPET_in_hpc(
  File "/home/c1755103/anaconda3/envs/cwld/lib/python3.11/site-packages/cuwalid/stopet/run_stoPET_inHPC.py", line 34, in run_stoPET_in_hpc
    extra_noise = mean_shift_rand_values(datapath, number_ensm, startyear, endyear)
                  ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/home/c1755103/anaconda3/envs/cwld/lib/python3.11/site-packages/cuwalid/stopet/stoPET_v2_4dryp.py", line 924, in mean_shift_rand_values
    ncmean=Dataset(os.path.join(datapath, 'meanshift_had.nc'))
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "src/netCDF4/_netCDF4.pyx", line 2521, in netCDF4._netCDF4.Dataset.__init__
  File "src/netCDF4/_netCDF4.pyx", line 2158, in netCDF4._netCDF4._ensure_nc_success
OSError: [Errno -51] NetCDF: Unknown file format: '/home/c1755103/naconda3/envs/cwld/lib/python3.11/site-packages/cuwalid/stopet/stopet_parameters/meanshift_had.nc'