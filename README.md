# Reading Instances

## Folder
Benchmark instances are found in `instances`.  The format of the filenames is `n-depot_position-request_distribution-seed` where `n` is the number of requests, `depot_position` denotes how the depot position was chosen, `request_distribution` describes how the requests are spacially distributed and `seed` differentiates between the three randomly generated instances for each combination of `depot_position` and `request_distribution`.

## How to Read Files
Each instance can be read into python via
```Python
import ast

with open(filename) as file_:
    instance_dict = ast.literal_eval(file_.read())

nodes = instance_dict['nodes']
F = instance_dict['F']
ct = instance_dict['ct']
cd = instance_dict['cd']
truck_cap = instance_dict['truck_cap']
drone_cap = instance_dict['drone_cap']
a = instance_dict['a']
b = instance_dict['b']
max_flight_time = instance_dict['max_flight_time']
ttt = instance_dict['ttt']
ttd = instance_dict['ttd']
```
where ```filename``` is the name of the instance.  Variable ```ttt``` is a list of lists such that ```ttt[i][j]``` gives the direct truck travel time from request i to j in minutes. Variable ```ttd``` is a list of lists such that ```ttd[i][j]``` gives the direct drone travel time from request i to j in minutes. Variables ```ct``` and ```cd``` give the truck and drone costs respectively ($/minute). Variables ```truck_cap``` and ```drone_cap``` give the load capacity of the truck and drone respectively.  Variable ```max_flight_time``` is the maximum flight time of a drone before its battery is depleted.  Variables ```a``` and ```b``` define the ratio of the truck and drone travel speeds.  For example, ```a=1``` and ```b=2``` would mean drones are twice as fast as trucks and have direct travel times that are half those of trucks.  Variable ```F``` is the fixed cost of using a truck-drone pair. Note that ```F``` is sufficiently large such that it is optimal to minimize the number of truck-drone pairs used.  Finally, ```nodes``` is a list of tuples, each giving the data for a request (or the depot).  The first element of the tuple gives the id, the second and third elements give the x and y coordinates of the request, the fourth and fifth give the start and end of the service time window for the request.  The sixth element is the request weight.  The final element is a boolean value that determines whether or not the request can be delivered by the drone.
