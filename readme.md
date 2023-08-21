# UNDERSTANDING ITLDIMS COMMAND

## Topics
- Setup
- Workings of the code
- Command Combinations
- Outputs of Command Combinations
- Current Priority

## Setup
- [Install etcd](https://etcd.io/docs/v3.4/install/) and create a single node etcd (locally, if needed) by running the `etcd` command
- Clone the [itldims-and-commands](https://github.com/yash-anand-fosteringlinux/itldims-and-commands/) and enter the 'Complete' directory.
- In the API directory, 'go run' the [main.go](https://github.com/yash-anand-fosteringlinux/itldims-and-commands/blob/main/Complete/etcd-inventory/main.go) for converting excel to CSV, uploading data to etcd & connecting with the API
- Run the `itldims` and `itldims get` related commands from the itldims directory.

# Workings of the code
- This code utilises a modifed version of  [main.go](https://github.com/yash-anand-fosteringlinux/itldimscmd/blob/main/api/main.go), where the etcd API url `localhost:8181/servers/` is connected with for displaying all the key-values.
- Data from the API Server is fetched and then the parsing of the data is done before the user inputs their argument/s to process the data from the API Server.
- `itldims` command is used to check connection with the API Server and `itldims get` subcommand is used to search user arguments from the API Server.
-  The method of placing user arguments into `localhost:8181/servers/<ServerType>/<ServerIP>/<Attribute>` is not used and grep like search is run through the data of `localhost:8181/servers`.
- If needed, user can search with a single key-component or value using `itldims get <input 1>`. The input entered by the user are then searched for and the key-values not needed are filtered out from the data in `localhost:8181/servers/`.

# Command Combinations
| S. No. | Command Combination               | Output Description                                      | Use-Case |
|-------|-----------------------------------|---------------------------------------------------------|------------|
| 01| `itldims` | Displays a message to tell if conection was made with API or not | User can learn if the API is running in background |
| 02| `itldims get servers`              | Displays all the running Servers with their Server IPs | Helps user see all the running servers |
| 03| `itldims get types`       | Displays all the running Server Types | Helps User find all the server types |
| 04| `itldims get attributes`         | Displays all Attributes   | Helps User find all the attributes |
| 05| `itldims get <Server IP>`         | Displays all Attribute values of a specific Server IP  | Helps user find values of a specific server IP|
| 06| `itldims get <server Type>`         | Displays values of a specific server Type  | User can find values of a specific server Type |
| 07| `itldims get <Attribute>`   | Displays values of a specific Attribute   | User can find all the RAMs of all servers |
| 08| `itldims get <Server IP/Type> <attribute>` | Displays all value of attribute from specific server Type/IP | User can find if any attribute is 'None' on '10.249.221.22' |
| 09| `itldims get <Server IP/Type/Attribute> <Value>` | Displays all Server IPs containing a specific value  | User can find if any attribute is 'None' on '10.249.221.22' |
| 10| `itldims get <value>` | Displays the Server IP & Attribute of the searched Value | Helps user learn about server Information related to a value like 'vahanapp05' |

## Outputs of Command Combinations
The possible combinations along with their outputs for the `itldims get` command have been provided below. For any output which is too lengthy, `. . . . .` has been used at the end to signify that the mentioned output gives complete data but is not being shown here completely.

**1. `itldims`to get the following output:**
1.1. If API is running
```
Connected to API. Interaction with etcd can be done.
```
1.2. If API is not running
```
Failed to connect to the etcd API.
```


**2. `itldims get servers`to get the following output:**
```
10.246.40.139
----------------------------
10.246.40.152
----------------------------
10.246.40.142
----------------------------
10.249.221.22
----------------------------
10.249.221.21
----------------------------
```

**3. `itldims get types` to get the following output:**
```
Physical
----------------------------
VM
----------------------------
```

**4. `itldims get attributes` to get the following output:**
```
LVM
----------------------------
NFS
----------------------------
Hostname
----------------------------
Gateway
----------------------------
PV
----------------------------
External_Disk
----------------------------
RAM
----------------------------
API
----------------------------
Internal_Partition
----------------------------
CPU
----------------------------
Environment
----------------------------
Netmask
----------------------------
External_Partition
----------------------------
data
----------------------------
Application
----------------------------
Internal_Disk
----------------------------
VG
----------------------------
OS
----------------------------
```

**5. `itldims get <Server IP>` or `itldims get 10.249.221.22`  to get the following output:**
```
Environment:
Production
----------------------------

PV:
PV Name=/dev/sda3
PV Size=101.00g
PV Name=/dev/sdb
PV Size=500.00g
----------------------------

Netmask:
255.255.255.128
----------------------------

RAM:
32GB
----------------------------

Gateway:
10.249.221.1
----------------------------

External_Partition:
u01:322GB
----------------------------

CPU:
8
----------------------------
. . . . .
```
    
**6. `itldims get <Server Type>` or `itldims get VM` to get the following output:**
```
Server IP: 10.249.221.21
Application:checkpost
----------------------------

Server IP: 10.249.221.22
OS:RHEL 8.7
----------------------------

Server IP: 10.249.221.22
External_Partition:u01:322GB
----------------------------
. . . . .
```

**7. `itldims get <Attribute>` or `itldims get RAM` to get the following output:**
```
Server IP: 10.249.221.22
RAM:32GB
----------------------------

Server IP: 10.246.40.142
RAM:32GB
----------------------------

Server IP: 10.249.221.21
RAM:32GB
----------------------------

Server IP: 10.246.40.139
RAM:32GB
----------------------------

Server IP: 10.246.40.152
RAM:32GB
----------------------------
```
    
**8. `itldims get <Server IP/Type> <attribute>`  or `itldims get 10.249.221.22 RAM`  to get the following output:**
```
RAM:
32GB
----------------------------
```

         
**9. `itldims get <Server IP/Type> <attribute>`  or `itldims get RAM 32GB`  to get the following output:**
```
Server IP: 10.246.40.152
RAM:32GB
----------------------------

Server IP: 10.249.221.21
RAM:32GB
----------------------------

Server IP: 10.249.221.22
RAM:32GB
----------------------------

Server IP: 10.246.40.142
RAM:32GB
----------------------------
```

**10. `itldims get <value>`or `itldims get vahanapp05` to get the following output:**
```
Server IP: 10.246.40.142
Hostname:vahanapp05
----------------------------
```
