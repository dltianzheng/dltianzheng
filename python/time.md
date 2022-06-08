```
#coding=utf-8

import pytz
CN = pytz.country_timezones['cn']
CN_tzinfo = pytz.timezone(CN[0])

if __name__ == '__main__':
    import datetime
    #无时区替换tzinfo 导致 ValueError: astimezone() cannot be applied to a naive datetime
    now = datetime.datetime.utcnow()
    print now
    print now.astimezone(CN_tzinfo)

```
- 有tzinfo的datetime需要修改时区
https://stackoverflow.com/questions/4563272/how-to-convert-a-utc-datetime-to-a-local-datetime-using-only-standard-library	