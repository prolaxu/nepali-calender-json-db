# Nepali Calendar API

A free, open-source REST API for Nepali calendar data with complete panchang (astrological) information. Data is served as static JSON files hosted on GitHub Pages.

## 🚀 Quick Start

### Base URL

```
https://prolaxu.github.io/nepali-calender-json-db/
```

### API Endpoints

#### Get Single Date

```
GET /{year}/{month}/{day}.json
```

**Example:**

```bash
curl https://prolaxu.github.io/nepali-calender-json-db/2082/01/15.json
```

#### Get Full Month

```
GET /{year}/{month}.json
```

**Example:**

```bash
curl https://prolaxu.github.io/nepali-calender-json-db/2082/01.json
```

#### Get Full Year

```
GET /{year}.json
```

**Example:**

```bash
curl https://prolaxu.github.io/nepali-calender-json-db/2082.json
```

## 📊 Data Model

### Single Date Response

```json
{
  "nepali_date": {
    "formated": "२ वैशाख २०८२, मंगलवार",
    "day": "२",
    "month": "वैशाख",
    "year": "२०८२",
    "day_name": "मंगलवार",
    "date": "2082-01-02"
  },
  "english_date": {
    "formated": "April 15, 2025",
    "day": "15",
    "month": "April",
    "year": "2025",
    "day_name": "Tuesday",
    "date": "2025-04-15"
  },
  "nepali_sambat": {
    "formated": "1145 चौलागा द्वितीया - 17",
    "year": "1145",
    "month": "चौलागा",
    "tithi": "द्वितीया - 17"
  },
  "event": "विश्व कला दिवस",
  "is_holiday": false,
  "panchang": {
    "surya": "5:41☀️, 18:29🌤",
    "chandra": "8:46 PM☽, 6:40 AM☾",
    "tithi": "द्वितीया upto 11:11:25, उपरान्त: तृतीया",
    "pakshya": "बैशाख कृष्ण पक्ष 🌖",
    "nakshatra": "विशाखा upto 27:26:23, उपरान्त: अनुराधा",
    "yoga": "सिद्धि upto 23:48:8, उपरान्त: व्यतीपात",
    "karan": "गर upto 11:11:25",
    "chandra_rashi": "तुला ♎ upto 20:42:30, उपरान्त: वृश्चिक ♏",
    "dinman": "32 घडी 0 पला - 12hr 48min",
    "ritu": "वसन्त - Spring",
    "ayan": "उत्तरायण"
  }
}
```

### Field Descriptions

#### `nepali_date` Object

| Field      | Type   | Description                                                    |
| ---------- | ------ | -------------------------------------------------------------- |
| `formated` | string | Human-readable Nepali date with Nepali numerals                |
| `day`      | string | Day in Nepali numerals (०-३२)                                  |
| `month`    | string | Nepali month name (वैशाख, जेठ, etc.)                           |
| `year`     | string | Year in Nepali numerals (२०८२)                                 |
| `day_name` | string | Day name in Nepali (आइतबार, सोमबार, etc.)                      |
| `date`     | string | Machine-readable date in YYYY-MM-DD format with English digits |

#### `english_date` Object

| Field      | Type   | Description                                   |
| ---------- | ------ | --------------------------------------------- |
| `formated` | string | Human-readable English date (Month Day, Year) |
| `day`      | string | Day of month (1-31)                           |
| `month`    | string | Full month name (January, February, etc.)     |
| `year`     | string | Year (2025, 2026, etc.)                       |
| `day_name` | string | Full day name (Monday, Tuesday, etc.)         |
| `date`     | string | ISO 8601 date format (YYYY-MM-DD)             |

#### `nepali_sambat` Object

| Field      | Type   | Description                           |
| ---------- | ------ | ------------------------------------- |
| `formated` | string | Complete Nepali Sambat representation |
| `year`     | string | Sambat year (e.g., "1145")            |
| `month`    | string | Sambat month name                     |
| `tithi`    | string | Sambat tithi information              |

#### Root Fields

| Field        | Type    | Description                                     |
| ------------ | ------- | ----------------------------------------------- |
| `event`      | string  | Special event or observance for the day         |
| `is_holiday` | boolean | Whether the day is a public holiday or Saturday |

#### `panchang` Object (Astrological Data)

| Field           | Type   | Description                            |
| --------------- | ------ | -------------------------------------- |
| `surya`         | string | Sunrise and sunset times with emojis   |
| `chandra`       | string | Moonrise and moonset times with emojis |
| `tithi`         | string | Lunar day with timing information      |
| `pakshya`       | string | Lunar fortnight (शुक्ल/कृष्ण पक्ष)     |
| `nakshatra`     | string | Lunar mansion with transition timing   |
| `yoga`          | string | Astrological yoga with timing          |
| `karan`         | string | Half-day period with timing            |
| `chandra_rashi` | string | Moon sign with transition timing       |
| `dinman`        | string | Day duration in घडी and पला            |
| `ritu`          | string | Season (वसन्त, ग्रीष्म, etc.)          |
| `ayan`          | string | Sun's path (उत्तरायण/दक्षिणायण)        |

## 💻 Usage Examples

### JavaScript (Fetch API)

```javascript
// Get single date
async function getDate(year, month, day) {
  const response = await fetch(
    `https://prolaxu.github.io/nepali-calender-json-db/${year}/${month
      .toString()
      .padStart(2, "0")}/${day.toString().padStart(2, "0")}.json`
  );
  return await response.json();
}

// Example usage
const date = await getDate(2082, 1, 15);
console.log(date.nepali_date.formated); // "१५ वैशाख २०८२, शुक्रबार"
console.log(date.event); // Event name
console.log(date.panchang.tithi); // Tithi information
```

### JavaScript (Get Full Month)

```javascript
async function getMonth(year, month) {
  const response = await fetch(
    `https://prolaxu.github.io/nepali-calender-json-db/${year}/${month
      .toString()
      .padStart(2, "0")}.json`
  );
  return await response.json();
}

// Get all dates in Baisakh 2082
const monthDates = await getMonth(2082, 1);
monthDates.forEach((date) => {
  console.log(date.nepali_date.formated, "-", date.event);
});
```

### Python

```python
import requests

# Get single date
def get_date(year, month, day):
    url = f"https://{prolaxu}.github.io/{nepali-calender-json-db}/{year}/{month:02d}/{day:02d}.json"
    return requests.get(url).json()

# Example
date = get_date(2082, 1, 15)
print(date['nepali_date']['formated'])
print(f"Holiday: {date['is_holiday']}")
print(f"Tithi: {date['panchang']['tithi']}")
```

### cURL

```bash
# Get specific date
curl -s https://prolaxu.github.io/nepali-calender-json-db/2082/01/15.json | jq '.nepali_date.formated'

# Get full month
curl -s https://prolaxu.github.io/nepali-calender-json-db/2082/01.json | jq '.[0].event'

# Get year
curl -s https://prolaxu.github.io/nepali-calender-json-db/2082.json | jq 'length'
```

## 📁 Repository Structure

```
.
├── 2082.json                 # Full year data (all 12 months)
├── 2082/
│   ├── 01.json              # Baisakh month (all dates)
│   ├── 01/
│   │   ├── 01.json          # Individual day files
│   │   ├── 02.json
│   │   └── ...
│   ├── 02.json              # Jestha month
│   ├── 02/
│   │   └── ...
│   └── ...
├── 2083.json
├── 2083/
│   └── ...
└── README.md
```

## 🗓️ Month Numbers

| Month No. | Nepali Name      | English Equivalent |
| --------- | ---------------- | ------------------ |
| 01        | वैशाख (Baisakh)  | April-May          |
| 02        | जेठ (Jestha)     | May-June           |
| 03        | असार (Ashad)     | June-July          |
| 04        | श्रावण (Shrawan) | July-August        |
| 05        | भदौ (Bhadra)     | August-September   |
| 06        | आश्विन (Ashwin)  | September-October  |
| 07        | कार्तिक (Kartik) | October-November   |
| 08        | मंसिर (Mangsir)  | November-December  |
| 09        | पुष (Poush)      | December-January   |
| 10        | माघ (Magh)       | January-February   |
| 11        | फाल्गुन (Falgun) | February-March     |
| 12        | चैत्र (Chaitra)  | March-April        |

## ⚡ Features

- **✅ No Rate Limits** - Static JSON files, unlimited requests
- **✅ Free Forever** - Hosted on GitHub Pages
- **✅ Complete Panchang** - 11 astrological fields per date
- **✅ Multiple Formats** - Access by day, month, or year
- **✅ CORS Enabled** - Use directly from browser
- **✅ Fast & Reliable** - Served via GitHub's CDN
- **✅ Offline Support** - Download and use locally

## 🔧 CORS Support

All endpoints support CORS and can be accessed directly from browser applications:

```javascript
// No CORS issues!
fetch("https://prolaxu.github.io/nepali-calender-json-db/2082/01/15.json")
  .then((res) => res.json())
  .then((data) => console.log(data));
```

## 📦 Available Years

- **2082** BS (2025-2026 AD)
- _(Add more years as they become available)_

## 🤝 Contributing

This is a static data repository. For issues with data accuracy or to request additional years, please visit the [scraper repository](https://github.com/your-username/hamro-patro-calender-scraper).

## 📜 License

This data is provided as-is for public use. While the API is free, please credit this repository if you use it in your project.

## 🔗 Related Projects

- [Calendar Scraper](https://github.com/your-username/hamro-patro-calender-scraper) - The tool used to generate this data
- Data Source: [Hamro Patro](https://www.hamropatro.com/) & [Ashesh Panchang](https://www.ashesh.com.np/)

## ⚠️ Disclaimer

This data is scraped from publicly available sources and provided for convenience. For official calendar information, please refer to the original sources.

---

**Made with ❤️ for the Nepali community**
