@startuml

class Taws {
  armed
  config: TawsConfig
  AlertSystem1: AlertSystem
  AlertSystem2: AlertSystem
  ...
  AlertSystemN: AlertSystem
  arm()
  disarm()
  inhibit()
  uninhibit()
  process(Aircraftstate): AlertState
}

class Aircraftstate {
  timestamp
  altitude
  altitude_ground
  climb_rate
  position_lat
  position_lon
  speed_ground
  speed_air
  heading
  pitch
  roll
  steep_approach_selected
  normalize()
}

class TawsConfig {
  max_climbrate
  max_climbrate_change
}

class AlertState {
  all_alerts: list(Alert, Alertlevel)
  alerts_total_count(): usize
  insert(Alert, AlertLevel)
}

interface AlertSystem {
  is_armed()
  arm()
  disarm()
  inhibit()
  uninhibit()
  is_inhibited()
  process(Aircraftstate): AlertLevel
}

Taws -> Aircraftstate
Taws --> AlertState
TawsConfig -o Taws

AlertSystem -> Aircraftstate

@enduml