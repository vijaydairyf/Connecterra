# Connecterra - Cow and Sensor Tracking system.

- The application is created using .net core and EntityFramework core and database in Microsoft SQL.
- The application has a standard SQL database with 4 tables: DBname as farmDB.
    - [dbo].[Audits]
    - [dbo].[Cows]
    - [dbo].[Farms]
    - [dbo].[Sensors]

- DbContext in Start up is using SQL Server and the connection string is present in DefaultConnection (appsettings.json). 

- There was an initial migration to the table using Microsoft.EntityFrameworkCore.Design. This was added to the API project for migration.

- Commands used in visual studio developer command prompt to create the database and the tables in SQL are as follows. 

    - dotnet ef migrations add InitialCreate -p Infrastructure -s API -c FarmContext
    - dotnet ef database update -p Infrastructure -s API -c FarmContext

- I have created a FarmContextSeed class, which will feed some mocked data to the database after running the solution. This will check if the tables are empty only then the data will be fed in.  This is reading the data from json files present in Infrastructure/SeedData.

- There are a total of 4 APIs created with multiple operations.

    Audit

    - GET  ​/api​/Audit - Get Audit List

    Cows

    - GET  ​/api​/Cows - Get list of cows
    - GET  ​/api​/Cows​/{id} - Get Cow based on cow ID
    - PUT ​/api​/Cows​/{cowId} - Update the cow's status based on CowId
    - GET  ​/api​/Cows​/count - Get Cow count base on farm , state and Date

    Farm

    - GET  ​/api​/Farm - Get list of Farms

    Sensors

    - GET  ​/api​/Sensors - Get list of Sensors
    - POST ​/api​/Sensors - Add a Sensor
    - GET  ​/api​/Sensors​/{id} - Get Sensor based on Sensor ID
    - PUT ​/api​/Sensors​/{sensorId} - Update a Sensor
    - GET  ​/api​/Sensors​/average - Get Sensor Average per month
    - GET  ​/api​/Sensors​/count - Get Sensor Count per month

- There is swagger implementation for the API to know the Request and Response with status code in details. Available in Json and can also access after running the application.
    - The local url for swagger - https://localhost:5001/swagger/index.html
    - The json is copied and available in (Documents/swagger.json) path. Copy the json to https://editor.swagger.io/ to view the APIs and its operations.

- I have created a Postman collection for the APIs available at (Documents/Connecterra(Cow and Sensor tracking).postman_collection).

## Architecture Diagram of the API implementation.
[![](https://mermaid.ink/img/eyJjb2RlIjoiZ3JhcGggVERcbiAgQVtDb250cm9sbGVyXSAtLT58R2V0IGRhdGEgZnJvbSBEYXRhUHJvdmlkZXJ8IEIoRGF0YVByb3ZpZGVyKVxuICBCIC0tPiB8R2V0IGRhdGEgZnJvbSBDb250ZXh0fCBDKFVuaXRPZldvcmspXG4gIEMgLS0-fEZhcm0vQ293L1NlbnNvci9BdWRpdHwgRChSZXBvc2l0b3J5KVxuICBEIC0tPiB8R2VuZXJpY1JlcG9zaXRvcnl8IEdbQ29udGV4dF1cbiAgRyAtLT4gfEdldCBkYXRhIGZyb20gRGF0YWJhc2V8SChEYXRhYmFzZSlcbiAgQyAtLT58U2F2ZUNoYW5nZXN8IEUoQ29tcGxldGUpXG4gIEUgLS0-fEF1ZGl0IGRldGFpbHMgYmVmb3JlIFNhdmluZ3wgRltDb250ZXh0LlNhdmVDaGFuZ2VzXVxuICBGIC0tPiB8U2F2ZSBBdWRpdCBkZXRhaWxzIGFmdGVyIFNhdmVDaGFuZ2VzfCBIKERhdGFiYXNlKVxuXG5cdFx0IiwibWVybWFpZCI6eyJ0aGVtZSI6ImRlZmF1bHQiLCJ0aGVtZVZhcmlhYmxlcyI6eyJiYWNrZ3JvdW5kIjoid2hpdGUiLCJwcmltYXJ5Q29sb3IiOiIjRUNFQ0ZGIiwic2Vjb25kYXJ5Q29sb3IiOiIjZmZmZmRlIiwidGVydGlhcnlDb2xvciI6ImhzbCg4MCwgMTAwJSwgOTYuMjc0NTA5ODAzOSUpIiwicHJpbWFyeUJvcmRlckNvbG9yIjoiaHNsKDI0MCwgNjAlLCA4Ni4yNzQ1MDk4MDM5JSkiLCJzZWNvbmRhcnlCb3JkZXJDb2xvciI6ImhzbCg2MCwgNjAlLCA4My41Mjk0MTE3NjQ3JSkiLCJ0ZXJ0aWFyeUJvcmRlckNvbG9yIjoiaHNsKDgwLCA2MCUsIDg2LjI3NDUwOTgwMzklKSIsInByaW1hcnlUZXh0Q29sb3IiOiIjMTMxMzAwIiwic2Vjb25kYXJ5VGV4dENvbG9yIjoiIzAwMDAyMSIsInRlcnRpYXJ5VGV4dENvbG9yIjoicmdiKDkuNTAwMDAwMDAwMSwgOS41MDAwMDAwMDAxLCA5LjUwMDAwMDAwMDEpIiwibGluZUNvbG9yIjoiIzMzMzMzMyIsInRleHRDb2xvciI6IiMzMzMiLCJtYWluQmtnIjoiI0VDRUNGRiIsInNlY29uZEJrZyI6IiNmZmZmZGUiLCJib3JkZXIxIjoiIzkzNzBEQiIsImJvcmRlcjIiOiIjYWFhYTMzIiwiYXJyb3doZWFkQ29sb3IiOiIjMzMzMzMzIiwiZm9udEZhbWlseSI6IlwidHJlYnVjaGV0IG1zXCIsIHZlcmRhbmEsIGFyaWFsIiwiZm9udFNpemUiOiIxNnB4IiwibGFiZWxCYWNrZ3JvdW5kIjoiI2U4ZThlOCIsIm5vZGVCa2ciOiIjRUNFQ0ZGIiwibm9kZUJvcmRlciI6IiM5MzcwREIiLCJjbHVzdGVyQmtnIjoiI2ZmZmZkZSIsImNsdXN0ZXJCb3JkZXIiOiIjYWFhYTMzIiwiZGVmYXVsdExpbmtDb2xvciI6IiMzMzMzMzMiLCJ0aXRsZUNvbG9yIjoiIzMzMyIsImVkZ2VMYWJlbEJhY2tncm91bmQiOiIjZThlOGU4IiwiYWN0b3JCb3JkZXIiOiJoc2woMjU5LjYyNjE2ODIyNDMsIDU5Ljc3NjUzNjMxMjglLCA4Ny45MDE5NjA3ODQzJSkiLCJhY3RvckJrZyI6IiNFQ0VDRkYiLCJhY3RvclRleHRDb2xvciI6ImJsYWNrIiwiYWN0b3JMaW5lQ29sb3IiOiJncmV5Iiwic2lnbmFsQ29sb3IiOiIjMzMzIiwic2lnbmFsVGV4dENvbG9yIjoiIzMzMyIsImxhYmVsQm94QmtnQ29sb3IiOiIjRUNFQ0ZGIiwibGFiZWxCb3hCb3JkZXJDb2xvciI6ImhzbCgyNTkuNjI2MTY4MjI0MywgNTkuNzc2NTM2MzEyOCUsIDg3LjkwMTk2MDc4NDMlKSIsImxhYmVsVGV4dENvbG9yIjoiYmxhY2siLCJsb29wVGV4dENvbG9yIjoiYmxhY2siLCJub3RlQm9yZGVyQ29sb3IiOiIjYWFhYTMzIiwibm90ZUJrZ0NvbG9yIjoiI2ZmZjVhZCIsIm5vdGVUZXh0Q29sb3IiOiJibGFjayIsImFjdGl2YXRpb25Cb3JkZXJDb2xvciI6IiM2NjYiLCJhY3RpdmF0aW9uQmtnQ29sb3IiOiIjZjRmNGY0Iiwic2VxdWVuY2VOdW1iZXJDb2xvciI6IndoaXRlIiwic2VjdGlvbkJrZ0NvbG9yIjoicmdiYSgxMDIsIDEwMiwgMjU1LCAwLjQ5KSIsImFsdFNlY3Rpb25Ca2dDb2xvciI6IndoaXRlIiwic2VjdGlvbkJrZ0NvbG9yMiI6IiNmZmY0MDAiLCJ0YXNrQm9yZGVyQ29sb3IiOiIjNTM0ZmJjIiwidGFza0JrZ0NvbG9yIjoiIzhhOTBkZCIsInRhc2tUZXh0TGlnaHRDb2xvciI6IndoaXRlIiwidGFza1RleHRDb2xvciI6IndoaXRlIiwidGFza1RleHREYXJrQ29sb3IiOiJibGFjayIsInRhc2tUZXh0T3V0c2lkZUNvbG9yIjoiYmxhY2siLCJ0YXNrVGV4dENsaWNrYWJsZUNvbG9yIjoiIzAwMzE2MyIsImFjdGl2ZVRhc2tCb3JkZXJDb2xvciI6IiM1MzRmYmMiLCJhY3RpdmVUYXNrQmtnQ29sb3IiOiIjYmZjN2ZmIiwiZ3JpZENvbG9yIjoibGlnaHRncmV5IiwiZG9uZVRhc2tCa2dDb2xvciI6ImxpZ2h0Z3JleSIsImRvbmVUYXNrQm9yZGVyQ29sb3IiOiJncmV5IiwiY3JpdEJvcmRlckNvbG9yIjoiI2ZmODg4OCIsImNyaXRCa2dDb2xvciI6InJlZCIsInRvZGF5TGluZUNvbG9yIjoicmVkIiwibGFiZWxDb2xvciI6ImJsYWNrIiwiZXJyb3JCa2dDb2xvciI6IiM1NTIyMjIiLCJlcnJvclRleHRDb2xvciI6IiM1NTIyMjIiLCJjbGFzc1RleHQiOiIjMTMxMzAwIiwiZmlsbFR5cGUwIjoiI0VDRUNGRiIsImZpbGxUeXBlMSI6IiNmZmZmZGUiLCJmaWxsVHlwZTIiOiJoc2woMzA0LCAxMDAlLCA5Ni4yNzQ1MDk4MDM5JSkiLCJmaWxsVHlwZTMiOiJoc2woMTI0LCAxMDAlLCA5My41Mjk0MTE3NjQ3JSkiLCJmaWxsVHlwZTQiOiJoc2woMTc2LCAxMDAlLCA5Ni4yNzQ1MDk4MDM5JSkiLCJmaWxsVHlwZTUiOiJoc2woLTQsIDEwMCUsIDkzLjUyOTQxMTc2NDclKSIsImZpbGxUeXBlNiI6ImhzbCg4LCAxMDAlLCA5Ni4yNzQ1MDk4MDM5JSkiLCJmaWxsVHlwZTciOiJoc2woMTg4LCAxMDAlLCA5My41Mjk0MTE3NjQ3JSkifX0sInVwZGF0ZUVkaXRvciI6ZmFsc2V9)]


1 - The state changes are reflected in the database by external services and APIs, i.e. someone from the app can change the sensor state to "Deployed" or some automation on the farm can change the cow state to "Pregnant".
   The API which can be used to achieve this is implemented under 
   - PUT ​/api​/Cows​/{cowId} - Update the cow's status based on CowId
   - PUT ​/api​/Sensors​/{sensorId} - Update a Sensor status

These changes are happening on a regular basis, i.e. multiple times a day from various sources. Sometimes errors may be committed as well, e.g., the cow's state can change from Pregnant to Dry and back to Pregnant within the same day. Typically cow state changes and sensor state changes occur after multiple days, so any quick changes happening in succession are generally erroneous and need to be flagged. 
     The API which can be used to achieve this is implemented under 
   - PUT ​/api​/Cows​/{cowId} - Update the cow's status based on CowId
   - PUT ​/api​/Sensors​/{sensorId} - Update a Sensor status
   - There is a RecordFlag property in both Cows and Sensors table which is updated to Error if there is any quick changes happening in succession.
   - This is achieved by checking the audit details of that record on that particular date. If there is a audit record then the flag is set to Error.

    
Part 1. You need to design an architecture for tracking this historical state, then implement it. Use your choice of database, microservice, language, platform, etc. technology. Would you update the existing database with any additional fields? If so, how would you index them? Additionally you may choose not to use the existing database to track these changes. If so, what kind of a mechanism would you use? How would you listen for these changes?

- I have used EntityFrameworkCore ChangeTracker to achieve the Audit trail of the data update and create. As part of this implementation I have created an Audit table and stored the audit details in that table whenever there is a change in state of Cow and Sensor.


Part 2. You also need to write a simple API that can answer the questions listed above.

1. How many cows are pregnant on farm "A" on a specific date? 
    - The API which can be used to achieve this is implemented under  - GET  ​/api​/Cows​/count - Get Cow count based on farm ,state and Date.
    - This is achieved by checking the audit details.
2. How many sensors died in June across the platform?
    - The API which can be used to achieve this is implemented under  - GET  ​/api​/Sensors​/count - Get Sensor Count based on month and status
    - This is achieved by checking the audit details.
3. On average how many new sensors are deployed every month in 2020?
    - The API which can be used to achieve this is implemented under - GET  ​/api​/Sensors​/average - Get Sensor Average based on year and status
    - This is achieved by checking the audit details.
    
    
    
## Future Improvement
- If provided with more time i could write more Unit tests for more code coverage.
- Create custom AuditDto to return user friendly response for GetAuditList operation.
