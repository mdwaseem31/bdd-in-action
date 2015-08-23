## chapter-2

- This code can be downloaded from [here](https://github.com/bdd-in-action/chapter-2.git).

- We have modified the project as per our need.

- The project structure is like below

![01-project.png](screenshots/01-project.png)

- The stories are arranged inside **src/test/resources/stories** like below

![02-stories.png](screenshots/02-stories.png)

- To run the tests, run the command: **mvn verify**

- Above will generate report inside target/site/thucydides/index.html which will look like below

![03-report.png](screenshots/03-report.png)

### Importing project in IntelliJ

- Import this project "train-timestables" as maven project

- IntelliJ will recommend you to download JBehave plugin, so do that.

## Project Source Code Explanation

- We have defined **Line** model in which a line is defined as consisting of:
    - lineName: like Blue Line, Red Line, Pink Line, etc
    - departingFrom: like Loop, Western, Kenosha, etc..
    - stations: like all the stations that this line will stop at..

- We are assuming that there is some **_Timetable_** service which can provide us the following services.

**List<LocalTime> findArrivalTimes(Line line, String targetStation)**:
    - This service will tell the arrival times of _specific_ train coming from _specific_ station at _specific_ target station.
    - Eg: Brown line coming from Adams/Wabash arrives at Fullterton train station at 8:00am, 8:15am, 8:30am, etc..
    - Note that the **Line** object contains information about the Line type and its departure station
    - The **targetStation** is the station on which we are waiting for the train.

**List<Line> findLinesThrough(String departure, String destination)**:
    - This service will tell all the possible **Lines** that goes from a _specific_ departure to a _specific_ destination
    - Eg: The lines going from chicago-loop to halsted/division station will be Red and Blue lines

- We have created **_InMemoryTimeTableService_** as a mock implementation of this service.

- Then there is another service **itineraryService** which provides us the closest departure times for a given **travelTime** and given **departure and destination** station
    - List<LocalTime> findNextDepartures(String departure, String destination, LocalTime startTime)

- The unit tests are in Spock that basically tests the services using the mock data created in **InMemoryTimetableService**

## JUnit Test Runner

- In above section we mentioned that the "mvn verify" command will run all the tests. But we can 