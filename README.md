def compute_battery_health(present_capacity,rated_capacity):
    health_categories={
        "healthy":0'
        "replace":0,
        "failed":0,
    }
#calculate SOH percentage
    soh_percentage=100*present_capacity/rated_capacity
#classify battery based on SOH
    if soh_percentage>80:
       health_categories["healthy"]+=1
    elif soh_percentage>62:
          health_categories["replace"]+=1
    else:
          health_categories["failed"]+=1
  #create and return the health report
    health_report={
           "soh percentage":soh_percentage,
           "classification":health_categories,
           }
    return health_report

battery_data=[
    {"present_capacity":105,"rated_capacity":120},
    {"present_capacity":90,"rated_capacity":120},
    {"present_capacity":75,"rated_capacity":120},
    {"present_capacity":50,"rated_capacity":120},
    ]
for battery in battery_data:
    health_report=compute_battery_health(battery["present_capacity"],battery["rated_capacity"])
    print(f"\nBattery soh:{health_report['soh percentage']:2f}%")
    print(f"classification:")
    for category,count in health_report["classsification"].items():
        print(f"\t{category}:{count}")
    
