# Churn-Project
Managing Customer Churn using Data Analytics
<hr>

## Setup Instructions
1. Python 3 and the required packages (requirements.txt)
2. PostgreSQL
3. PgAdmin - for PostgreSQL database setup
<hr>
<details><summary><strong>Links for Downloading</strong></summary> <br>
For Linux : <br>
<ol> 
  <li> For installing Python: https://www.python.org/downloads/ </li>
  <li> For installing PostgreSQL: https://www.postgresql.org/download/linux/ </li>
  <li> For installing pgAdmin: https://www.pgadmin.org/download/pgadmin-4-apt/ </li>
</ol>
</details>
<hr>

## Database Setup 
Create a Database by clicking on the root of the Servers tree and selecting Create. <br>

<img width="360" alt="Database creation img" src="https://github.com/ShreejithSG/Churn-Project/assets/72182153/8ea41460-545d-4d12-a97d-058b6b9a3589"> <br>

A dialog will open. Name your connection localhost, and on the second tab (Connection) enter the address 127.0.0.1. You should also enter your user name and password. <br>

<img width="720" alt="Screenshot 2023-06-12 at 10 33 45 AM" src="https://github.com/ShreejithSG/Churn-Project/assets/72182153/2e0c1121-fb32-4bdc-a38d-d91d73fc5fa8"> <br>

Next you need to create a new database to hold all of the churn data schemas you create. You will probably create multiple schemas as you work on the examples in the book and/or your own data so this will help keep these organized. An easy way to create a database is in PgAdmin - right click on the Databases node under localhost in the tree: <br>

<img width="362" alt="Screenshot 2023-06-12 at 10 36 04 AM" src="https://github.com/ShreejithSG/Churn-Project/assets/72182153/3860afcf-0181-40b1-b454-d4b4ad728001"> <br>

And enter the name of the new database: <br>

<img width="360" alt="Screenshot 2023-06-12 at 10 36 38 AM" src="https://github.com/ShreejithSG/Churn-Project/assets/72182153/97b163e8-49e7-4e30-927c-b11698bb173a"> <br>
<hr>

## Code Setup

## Command Line Setup
### Create a Virtual Environment
First, you should make a new virtual environment in which to install the Fight Churn code.
```
python3 -m venv churn
```
You can use whatever name you like for the python environment but i have used churn for relevance. Next, you have to activate your environment!
<hr>

### Active environment 
```
source churn/bin/activate
```
The prompt will change to :
```
(churn) ~ user$ 
```
<hr>

### Install the fightchurn package
```
pip install fightchurn
```
<hr>

### Create a directory for output
You should make a local folder to store your output. On linux that would look as follows:
```
mkdir my_churn_output_folder
```
<hr>

### Start the Python virtual environment
Next you should start your Python environment, and enter a python shell:
```
source churn/bin/activate
python
```
All the commanda above are assuming you named your virtual environment churn). You should see something like the following...
```
(py_venv) :~ user$ python
Python 3.9.6 (default, Jun 29 2021, 05:25:02) 
[Clang 12.0.5 (clang-1205.0.22.9)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```
<hr>

### Import the run_churn_listing_module
Next, you will import the fightchurn package that you will use to run everything:
```
from fightchurn import run_churn_listing
```
<hr>

### Set the churn environment variables
Now you need to set a few enviroment variables. These are:

1. The database name : 'churn' in the example below
2. The username for the database
3. The password for the database
4. A local folder where outputs can be written....
```
run_churn_listing.set_churn_environment('churn','user','password','path_to_my_churn_output_folder')
```
<hr>

### Run the data simulation
Next, you need to write some data to the database in order to run the code against. The example is for a standard simulation of 10,000 customers. Use the following command :
```
run_churn_listing.run_standard_simulation(init_customers=10000)
```
You will see the output as follows : 
```
Creating schema socialnet7 (if not exists)...
Creating table event (if not exists)
Creating table subscription (if not exists)
Creating table event_type (if not exists)
Creating table metric (if not exists)
Creating table metric_name (if not exists)
Creating table active_period (if not exists)
Creating table observation (if not exists)
Creating table active_week (if not exists)
Creating table account (if not exists)

Creating 2000 initial customers for month of 2020-01-01
Simulated customer 0/2000: 2 subscriptions & 100 events
Simulated customer 100/2000: 448 subscriptions & 154,047 events
Simulated customer 200/2000: 872 subscriptions & 282,882 events
Simulated customer 300/2000: 1,324 subscriptions & 426,866 events
Simulated customer 400/2000: 1,767 subscriptions & 557,543 events
...
```
This will continue for a while - maybe 10-15 minutes if you ran the full 10,000 customer simulation.
<hr>

## Run code listings
Now you are ready to run the code. To do that you use the run_listing function that you previously imported. For example, the following is chapter 2, listing 2:
```
run_churn_listing.run_listing(2,2)
```
### Running multiple listings and versions
In some parts of the book you might want to run more than one listing at once. To do this, pass as a list for the listing argument. For example, to run all four chapter 2 churn calculation listings try:
```
run_churn_listing.run_listing(2,[1,2,3,4])
```
Later in the book, some of the listings have multiple versions with different arguments. The run_listing function also takes a version argument. For example, to run a query and plot the results of the events per day for the first event created by the simulation, try the following:
```
run_churn_listing.run_listing(chapter=3,listing=[9,10],version=[1,2,3])
```
That command should save the plots to your output directory.
