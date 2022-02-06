## Nepali Calender Json Db

This is simple and small JSON database of Nepali calendar events,festivals,tithe in different year.

## API Reference

#### Get item

```http
  GET https://raw.githubusercontent.com/prolaxu/nepali-calender-json-db/main/${year}/${month}.json
```

| Parameter | Type  | Description                                |
| :-------- | :---- | :----------------------------------------- |
| `year`    | `int` | **Required**. Year from calender to fetch  |
| `month`   | `int` | **Required**. Month from calender to fetch |

#### Example response

```
{
    {
   "event":"गौरी व्रत",
   "np":"२",
   "tithi":"तृतिया",
   "en":"15",
   "model":{
      "np_date":"२ वैशाख २०७८, बिहिवार ",
      "en_date":"April 15, 2021",
      "event":"गौरी व्रत",
      "panchang":"पञ्चाङ्ग: अयुश्मान गरीजी कृत्तिका"
   },
   .........
}
```
