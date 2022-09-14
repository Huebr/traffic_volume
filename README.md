# TrafficVolume

Our datasets can be found in the file my_data.rar in the following link:

https://drive.google.com/file/d/1I2HfeiJYSwTFTDEZEYhnkg6wSMio2D65/view?usp=sharing

The datasets are in the folder /data/outputs_tests/ separated by folder:
- daily: This folder has our traffic volume data for each date.
- new_instances: This folder has our teams schedules for each date and type.

The .Rmd file defines how we generated our instances just extract the in the root folder the data folder.

A julia code to demonstrate how to read the data:
```
  using CSV
  using Tables
  using LinearAlgebra
  data_path = "<your_path>//data//output_tests//"
  schedule_dirname = "new_instances//"
  instance_dirname = "daily//"
  total_time = 24
  instances_paths = readdir(string(data_path,instance_dirname); join=true)
  schedules_paths = readdir(string(data_path,schedule_dirname); join=true)
  viable_dates = readdir(string(data_path,schedule_dirname))
  for v in viable_dates
    Mu = CSV.File(string(data_path,instance_dirname,v,".csv"),select = [8:1:31;])|> Tables.matrix
    Mu_scalar = CSV.File(string(data_path,instance_dirname,v,".csv"),select = [34])|> Tables.matrix
    Mu = Mu_scalar.*Mu    
    schedule_partitions = readdir(string(data_path,schedule_dirname,v); join=true) 
    for s in schedule_partitions
      matrix = CSV.File(s,drop=["table"]) |> Tables.matrix
      n_locations = size(matrix,2)
      n_teams = floor(Int,size(matrix,1)/tempo_total)
      M = reshape(matrix,(n_teams,n_locations,total_time))
  end
``` 
Any problems please contact by email or here.


