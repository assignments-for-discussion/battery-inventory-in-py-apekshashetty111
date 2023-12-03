def compute_battery_health(present_capacity, rated_capacity):
    health_categories = {
      "Healthy": 0,
      "Replace": 0,
      "Failed": 0,
  }

  # Calculate SoH percentage
    soh_percentage = 100 * present_capacity / rated_capacity

  # Classify battery based on SoH
    if soh_percentage > 80:
       health_categories["Healthy"] += 1
    elif soh_percentage > 62:
        health_categories["Replace"] += 1
    else:
        health_categories["Failed"] += 1

  # Create and return the health report
    health_report = {
      "SoH percentage": soh_percentage,
      "Classification": health_categories,
  }
  return health_report


battery_data = [
    {"present_capacity": 105, "rated_capacity": 120},
    {"present_capacity": 90, "rated_capacity": 120},
    {"present_capacity": 75, "rated_capacity": 120},
    {"present_capacity": 50, "rated_capacity": 120},
]

for battery in battery_data:
  health_report = compute_battery_health(battery["present_capacity"], battery["rated_capacity"])
  print(f"\nBattery SoH: {health_report['SoH percentage']:.2f}%")
  print(f"Classification:")
  for category, count in health_report["Classification"].items():
    print(f"\t{category}: {count}")

