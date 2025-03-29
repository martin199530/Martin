# Splunk: Exploring SPL
Splunk is a powerful SIEM solution that provides the ability to search and explore machine data. Search Processing Language (SPL) is used to make the search more effective. It comprises various functions and commands used together to form complex yet effective search queries to get optimized results.

## Search & Reporting App 
It is the default interface used to search and analyze the data on the Splunk Home page. It has various functionalities that assist analysts in improving the search experience.

![Image](https://github.com/user-attachments/assets/a2e33968-11d4-484e-ae96-6d961aaea56d)

### 1. Search Head:
Search Head is where we use search processing language queries to look for the data.

![Image](https://github.com/user-attachments/assets/a887d644-93f7-41e9-8de7-0876579d0f64)

### 2. Time Duration:
This tab option provides multiple options to select the time duration for the search. All-time will display the events in real-time. Similarly, the last 60 minutes will display all the events captured in the last hour.

![Image](https://github.com/user-attachments/assets/ed2dd624-3273-432a-abf1-22c09c1f0819)

### 3. Search History:
This tab saves the search queries that the user has run in the past along with the time when it was run. It lets the user click on the past searches and look at the result. The filter option is used to search for the particular query based on the term.

![Image](https://github.com/user-attachments/assets/ccf71156-88b8-4f3b-b6c8-a73791b317cc)

### 4. Data Summary:
This tab provides a summary of the data type, the data source, and the hosts that generated the events as shown below. This tab is very important feature used to get a brief idea about the network visibility.

![Image](https://github.com/user-attachments/assets/b0f60ccd-7fb3-46db-be71-a1649af4627a)

### 5. Field Sidebar:

The Field Sidebar can be found on the left panel of Splunk search. This sidebar has two sections showing **selected fields** and **interesting fields**. It also provides quick results, such as top values and raw values against each field.

![Image](https://github.com/user-attachments/assets/e2847e21-b47b-4390-b886-4423802b60e9)

**Note:**  we will work on the 

      index=Windowslogs 

**Quetion 1 :** In the search History, what is the 7th search query in the list? (excluding your searches from today)

![Image](https://github.com/user-attachments/assets/080d7bbf-80eb-4b69-a29b-6acfd763e9d2)

      Answer : index=windowslogs | chart count(EventCode) by Image

**Question 2 :** In the left field panel, which Source IP has recorded max events?

![Image](https://github.com/user-attachments/assets/6a51be5f-3a33-421c-bbaf-35db6b90a844)

     Answer : 172.90.12.11

**Question 3 :** How many events are returned when we apply the time filter to display events on 04/15/2022 and Time from 08:05 AM to 08:06 AM?

![Image](https://github.com/user-attachments/assets/4de59ab9-18a3-45d2-b5dc-cd742d16e83f)

          Answer : 134

## Splunk Processing Language Overview

Splunk Search Processing Language comprises of multiple functions, operators and commands that are used together to form a simple to complex search and get the desired results from the ingested logs.

### Search Field Operators

Splunk field operators are the building blocks used to construct any search query. These field operators are used to filter, remove, and narrow down the search result based on the given criteria. Common field operators are **Comparison operators, wildcards,** and  **boolean operators**.

**Comparison Operators :** These operators are used to compare the values against the fields. Some common comparisons operators are mentioned below:

      Equal                         =
      Not Equal to                  !=
      Less than                     <
      Less than or Equal to         <=
      Greater than                  >
      Greater than or Equal to      >=

**earch Query:** 

      index=windowslogs AccountName !=SYSTEM

![Image](https://github.com/user-attachments/assets/4920b75b-3d8d-4702-866f-e27d892ac175)

**Boolean Operators :** Splunk supports the following Boolean operators, which can be very handy in searching/filtering and narrowing down results. **NOT, OR AND**.

﻿To understand how boolean operator works in SPL, lets add the condition to show the events from the James account.

**Search Query:** 

      index=windowslogs AccountName !=SYSTEM AND AccountName=James

![Image](https://github.com/user-attachments/assets/0001cb6e-bf55-439e-a1fd-bdb084f6c12d)

**Wild Card :**
Splunk supports wildcards to match the characters in the strings.

      Wildcard symbol  *   Example:  Statu=fail*

In the events, there are multiple DestinationIPs reported. Let's use the wildcard only to show the **DestinationIP** starting from 172.*

**Search Query:** 

      index=windowslogs DestinationIp=172.*

![Image](https://github.com/user-attachments/assets/06c68670-d4b2-4877-affb-86f8f186d0c4)

**Question 1 :** How many Events are returned when searching for Event ID 1 **AND** User as *James*?

![Image](https://github.com/user-attachments/assets/daff71f1-edc1-451a-898a-48b66b18c257)

      Answer : 4

**Question 2 :** What is the Source IP with highest count returned with this Search query?
**Search Query :** index=windowslogs  Hostname="Salena.Adam" DestinationIp="172.18.38.5"

![Image](https://github.com/user-attachments/assets/f0015f67-539d-4bc2-950e-72a28732df6b)

      Answer : 172.90.12.11

## Filtering the Results in SPL
Our network generates thousands of **logs** each minute, all ingesting into our **SIEM solution**. It becomes a daunting task to search for any anomaly without using filters. **SPL** allows us to use **Filters** to narrow down the result and only show the important events that we are interested in. We can add or remove certain data from the result using filters. The following commands are useful in applying filters to the search results.

### Fields

Fields command is used to add or remove mentioned fields from the search results. To remove the field, **minus sign ( - )** is used before the fieldname and **plus ( + )** is used before the fields which we want to display.

      Syntax       | fields <field_name1>  <field_name2>

      Example      | fields + HostName - EventID


Let's use the **fields** command to only display **host**, **User**, and **SourceIP** fields using the following syntax.

**Search Query:** index=windowslogs | fields + host + User + SourceIp

![Image](https://github.com/user-attachments/assets/061d3ca9-14ed-4796-82ef-17029a08daff)

### Search 

This command is used to search for the raw text while using the chaining command **|**

      Syntax        | search  <search_keyword>

      Example       | search "Powershell"

Use the **search** command to show all the events containing the term **Powershell**. This will return all the events that contain the term **"Powershell"**.

**Search Query**: index=windowslogs | search Powershell

![Image](https://github.com/user-attachments/assets/7a241582-c8be-4f4e-8bee-f029c6a0816b)


### Dedup
Dedup is the command used to remove duplicate fields from the search results. We often get the results with various fields getting the same results. These commands remove the duplicates to show the unique values.

      Syntax   | dedup <fieldname>

      Example  | dedup EventID

We can use the dedup command to show the list of unique EventIDs from a particular hostname.

**Search Query**: index=windowslogs | table EventID User Image Hostname | dedup EventID

![Image](https://github.com/user-attachments/assets/b95dfade-0636-46df-96b1-8cec8396bd64)

### Rename

It allows us to change the name of the field in the search results. It is useful in a scenario when the field name is generic or log, or it needs to be updated in the output.

      Syntax      | rename  <fieldname>
      
      Example     | rename User as Employees

Let's rename the User field to Employees using the following search query.

**Search Query**: index=windowslogs | fields + host + User + SourceIp | rename User as Employees

![Image](https://github.com/user-attachments/assets/d6874f74-c12f-4721-84cf-33d008c9eb4c)

## SPL - Structuring the Search Results

SPL provides various commands to bring structure or order to the search results. These sorting commands like **head, tail**, and **sort** can be very useful during logs investigation. These ordering commands are explained below:

### Table

Each event has multiple fields, and not every field is important to display. The **Table** command allows us to create a table with selective fields as columns.

      Syntax       | table <field_name1> <fieldname_2>  
      
      Example      | table
                   | head 20 # will return the top 20 events from the result list.
                
This search query will create a table with three columns selected and ignore all the remaining columns from the display.

**Search Query**: index=windowslogs | table EventID Hostname SourceName

![Image](https://github.com/user-attachments/assets/33efafc4-d344-47f4-bf6e-72d900f26d71)

### Head

The **head** command returns the first 10 events if no number is specified.

      Syntax     | head <number> 
  
      Example    | head       # will return the top 10 events from the result list   
                 | head 20    # will return the top 20 events from the result list

The following search query will show the table containing the mentioned fields and display only the top 5 entries.

**Search Query**: index=windowslogs |  table _time EventID Hostname SourceName | head 5

![Image](https://github.com/user-attachments/assets/1b903a19-2311-45e3-8266-7937fee49587)

### Tail

The **Tail** command returns the last 10 events if no number is specified.

      Syntax     | tail <number>   
      
      Example    | tail      # will return the last 10 events from the result list 
                 | tail 20   # will return the last 20 events from the result list

The following search query will show the table containing the mentioned fields and display only 5 entries from the bottom of the list.

**Search Query**: index=windowslogs |  table _time EventID Hostname SourceName | tail 5

![Image](https://github.com/user-attachments/assets/99f463e8-40c5-4216-897c-4631c5938d1e)

### Sort

The **Sort** command allows us to order the fields in ascending or descending order.

      Syntax      | sort <field_name>  
      
      Example     | sort Hostname # This will sort the result in Ascending order.

The following search query will sort the results based on the Hostname field.

**Search Query**: index=windowslogs |  table _time EventID Hostname SourceName | sort Hostname

![Image](https://github.com/user-attachments/assets/13b35b96-0577-423d-ae4f-d61f729a9d13)

### Reverse

The reverse command simply reverses the order of the events.

      Syntax   |  reverse
      
      Example   <Search Query> | reverse   

**Search Query**: index=windowslogs | table _time EventID Hostname SourceName | reverse  

![Image](https://github.com/user-attachments/assets/7c1867af-26da-4af7-8cac-31fe7197b354)

## Transformational Commands in SPL

Transformational commands are those commands that change the result into a data structure from the field-value pairs. These commands simply transform specific values for each event into numerical values which can easily be utilized for statistical purposes or turn the results into visualizations. Searches that use these transforming commands are called transforming searches. Some of the most used transforming commands are explained below.

### Top

This command returns frequent values for the top 10 events.

      Syntax     | top  <field_name>
                 | top limit=6 <field_name>

      Example    top limit=3 EventID

The following command will display the top 7 Image ( representing Processes) captured.

**Search Query**: index=windowslogs | top limit=7 Image

![Image](https://github.com/user-attachments/assets/92888cb8-cb1d-454b-b19b-22dcfa9878da)

### Rare 

This command does the opposite of top command as it returns the least frequent values or bottom 10 results.


      Syntax     | rare  <field_name>
                 | rare limit=6 <field_name>

      Example    rare limit=3 EventID

The following command will display the rare 7 Image ( representing Processes) captured.

**Search Query**: index=windowslogs | rare limit=7 Image

![Image](https://github.com/user-attachments/assets/dc5ea2a1-88a1-4d39-9b7d-9b4580b30d5c)

### Highlight

The highlight command shows the results in raw events mode with fields highlighted.

      Syntax   highlight      <field_name1>      <field_name2>
      
      Example   highlight User, host, EventID, Image

The following command will highlight the three mentioned fields in the raw logs

**Search Query**: index=windowslogs | highlight User, host, EventID, Image

![Image](https://github.com/user-attachments/assets/22546a5a-de49-4b7d-9022-6f4fbf011642)
![Image](https://github.com/user-attachments/assets/9d424a9c-0edb-4225-b4b3-8e00c4a01060)
## EndS
