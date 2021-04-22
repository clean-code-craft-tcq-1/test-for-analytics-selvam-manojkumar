# Test for Analytics

Design tests for Analytics functionality on a Battery Monitoring System.

Fill the parts marked '_enter' in the **Tasks** section below.

## Analysis-functionality to be tested

This section lists the Analysis for which _tests_ must be written.

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

## Tasks

### List Dependencies

List the dependencies of the Analysis-functionality.

1. Access to the Server containing the telemetrics in a csv file
1. interface or library to read the data from the csv files
1. threshold data of the battery to find the breach
1. interface or library to generate the pdf report
1. Access to the server to store the generated pdf report
1. Notification interfaces (access and details if required for notification) which has to be triggered once new report is avaialble


### Mark the System Boundary

What is included in the software unit-test? What is not? Fill this table.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|---
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | No            | This part is not developed as part of the software
Counting the breaches       | Yes           | This is part of the software being developed
Detecting trends            | Yes           | This is part of the software being developed
Notification utility        | No            | This part is not developed as part of the software

### List the Test Cases

Write tests in the form of `<expected output or action>` from `<input>` / when `<event>`

Add to these tests:

1. expected output: write file failed event: no write access for storing pdf report
1. Write minimum and maximum to the PDF from a csv containing positive and negative readings
1. Write "Invalid input" to the PDF when the csv doesn't contain expected data
1. Write "No Records/Data Found" to the PDF when the csv is empty
1. Write "Access denied to read csv" to the PDF when the access to csv is not available
1. Write "Battery specs not found" to the PDF when battery specifications(for instance threshold limit) are is not available
1. expected output : proper trend to be recorded with date&time event: when reading are increased for 30 minutes
1. expected output : no trend to be recorded event: when increase in reading for less than 30 minutes
1. expected output : notification to be triggered event: when pdf is generated
1. expected output : pdf report to be generated event: when a week is completed


### Recognize Fakes and Reality

Consider the tests for each functionality below.
In those tests, identify inputs and outputs.
Enter one part that's real and another part that's faked/mocked.

| Functionality            | Input        | Output                      | Faked/mocked part
|--------------------------|--------------|-----------------------------|---
Read input from server     | csv file     | internal data-structure     | Fake the server store
Validate input             | csv data     | valid / invalid             | None - it's a pure function
Notify report availability | notifcation details/pdf file          | notification trigger                      | mock
Report inaccessible server | invalid sever address | report with error message               | fake
Find minimum and maximum   | csv data | expected minimum/maximum                 | mock
Detect trend               | csv data | report with trend               | mock
Write to PDF               | internal data | pdf with data               | mock
