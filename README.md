# MySQL 

CREATE TABLE_flights
(Flights_id INT,
Airline VARCHAR(10),
Flight_Number INT,
Origin_Airport VARCHAR(10),
Destination_Airport VARCHAR(10),
Departure_Delay INT,
Air_Time INT,
Arrival_Time INT
)
where flights; 

select * from flights;

update flights
set destination_Airport = "VARCHAR(50)"
where Destination_Airport;

insert into Flights (Airline,Flight_Number,Origin_Airport,Destination_Airport,Departure_Delay,Air_Time,Arrival_Time)
values 
("VX","897","LAS","SFO","10","89","819"),
("MQ","2842","ATL","DSM","4","800","1115");

ALTER table flights
add Total_Airtime INT;

UPDATE flights
SET total_airtime = COALESCE(Air_Time, 0) + COALESCE(Arrival_Time, 0);

SELECT Departure_Delay,
 sum(total_airtime) over(order by departure_delay) as cumulative_time
 from flights;

SELECT 
    Airline,
    Flight_Number,
    Origin_Airport,
    Destination_Airport,
    Departure_Delay,
    Air_Time,
    Arrival_Time,
    SUM(Air_Time) OVER (ORDER BY Departure_Delay) AS Cumulative_AirTime
FROM flights;

SELECT
air_time,
arrival_time,
total_airtime,
case when total_airtime < 1000 then 'below 1000'
when total_airtime between 300 and 1000 then '300-1000'
when total_airtime between 1000 and 3000 then '1000-3000'
else 'above 1000'
end total_airtime
from flights

select max(Departure_Delay) AS SUM
from flights;

(SELECT avg(air_time) from flights);

select *
from flights AS f1 
inner join flights AS f2
on f1.destination_airport = f2.destination_airport;

alter table flights
drop column flights_id;
