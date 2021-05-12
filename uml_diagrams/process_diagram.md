@startuml

(*) -d> "Collect new sensor data"
 -d> "Create AircraftState"
note left
Contains infos like
timestamp, altitude, 
position, speed, heading, ...
end note
 -d> "Use TAWS.process(AircraftState)"
 -d> "Each AlertSystem processes
the new AircraftState"
 -> "Combine output of the
AlertSystems to new AlertState"
 -u> "Output AlertState"
note right
Gives a list of alerts
and their severity
end note
 -l> "Collect new sensor data"

@enduml