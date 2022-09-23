# neo4j Assignment
## Neo4j Enterprise Setup 
This guide assumes an active internet connection, and has been tested using the following software versions:
- VMWare Workstation 16 Player (16.2.4 build-20089737)
- Ubuntu 22.04.1 LTS amd64
- neo4j Enterprise 1:4.4.9

### Instructions

1. After powering on the virtual machine first confirm that no Java has been previously installed. If there has been a previous installation, the neo4j documentation has information on how to handle [^1] 
```shell
update-java-alternatives --list
```
2. Add the official OpenJDK package to apt
```shell
sudo add-apt-repository -y ppa:openjdk-r/ppa
sudo apt-get update
```
3. Add the neo4j repository to apt
```shell
wget -O - https://debian.neo4j.com/neotechnology.gpg.key | sudo apt-key add -
echo 'deb https://debian.neo4j.com stable 4.4' | sudo tee -a /etc/apt/sources.list.d/neo4j.list
sudo apt-get update
```
4. Confirm that ```neo4j/stable,stable 1:4.4.9 all``` is returned when you run the following command 
```shell
apt list -a neo4j
```
5. Run the following command to install neo4j Enterprise Edition [^2]
```shell
sudo apt-get install neo4j-enterprise=1:4.4.9
```
6. When prompted to continue enter ```Y```
7. When prompted to accept the licence agreement and you agree, press ```down``` on the keyboard and then ```Enter```
8. Run the following command to confirm that version 4.4.9 has been installed
```shell
neo4j version
```
9. Start neo4j by using the command [^3] Take note of the URL returned to the terminal
```shell
sudo neo4j start
```
10. After a couple of minutes confirm that neo4j is running by using the command
```shell
neo4j status
```
11. Navigate to the URL captured in task 9 using Firefox or your browser, and when prompted to login use ***neo4j*** as the username and password
![Login page](/assets/login.png)
12. Update your password when prompted
![Update password page](/assets/updatepassword.png)
13. You should now be connected via the neo4j Browser
![Connected](/assets/connected.png)




## Modelling Dataset
### Background
Retail North Wind Data
Describe application in detail, 
domain of application
#### Use Cases
- Anomalies in shipping with recipients outside of normal
- Re-targetting workforce to region with more Customers/Suppliers

ranked by importance
### Data model
The json file as exported from arrows.app is located [Data Model JSON](/NorthWind%20Retail%20DataSet.json)[^4]
![Data Model](/assets/datamodel_02.png)
### Instructions
1. Copy the files from the data directory to the Virtual Machine (git?)
2. Copy to the neo4j import directory /var/lib/neo4j/import
3. Start the neo4j service, once the Browser is available login using the password created in the earlier part
4. For each of the files test they can be read by using the following command, each table should return a count e.g.
```shell
LOAD CSV FROM "file:///northwind-categories.csv" AS line
RETURN count(*);
```
Full code [Full code](/cypher_checkfiles.txt)
5. Create the schema using the generated Cypher [Cypher Create Model](/cypher_createmodel.txt)
6. Run the Cypher queries (to be created and checked in) to create the nodes and relationships off the CSVs
### Use Cases - Cypher Queries with Results

## Graph Enabled Ingestion (Python)

## ~~Cypher Queries~~
[^1]: https://neo4j.com/docs/operations-manual/current/installation/linux/debian/#multiple-java-versions
[^2]: If the error ```E: dpkg was interrupted, you must manually run 'sudo dpkg --configure -a' to correct the problem.``` appears, run the command as instructed, and re-run the install command
[^3]: To review user permissions rather than using sudo...
[^4]: Maybe look at restructuring the directory
