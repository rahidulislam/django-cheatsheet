# Python datetime

### Get Days between two dates

[source link](https://www.w3resource.com/python-exercises/python-basic-exercise-14.php)
    
    from datetime import datetime
    
    dates = "2020-12-25".split("-")
    now = datetime.now()
    application_time = datetime(int(dates[0]), int(dates[1]), int(dates[2]))
    print("yes12")
    print(now.date())
    print(application_time.date())
    x = now.date()-application_time.date()
    print(x.days)

### Get list of days between two days

[source link](https://stackoverflow.com/questions/7274267/print-all-day-dates-between-two-dates/7274316)
