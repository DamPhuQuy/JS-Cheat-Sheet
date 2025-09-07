# JS Date

# Table of contents

- [JS Date](#js-date)
- [Table of contents](#table-of-contents)
  - [1. JS Time](#1-js-time)
    - [1.1. Date, Timestamp, ISO 8601](#11-date-timestamp-iso-8601)
    - [1.2. Basic Date methods](#12-basic-date-methods)
    - [1.3. getTime(), getTimezoneOffset()](#13-gettime-gettimezoneoffset)
    - [1.4. Convert Date object to string](#14-convert-date-object-to-string)
## 1. JS Time

### 1.1. Date, Timestamp, ISO 8601

```javascript
// Date
// Timestamp: UTC (ms)
// ISO 8601

// Date and time expressed according to Timestamp
console.log(Date.parse("2024-01-01T10:00:00.200Z")); // 17041103200200 (ms)

// Date and time expressed according to ISO 8601
// Date in UTC: 2025-09-07 (YYYY-MM-DD)
// Time in UTC: 02:04:08.200Z (HH:MM:SS.MS)
// Time in UTC+7: 02:04:08.200+07:00
// Date and time in UTC: 2025-09-07T02:04:08Z.200

// create a Date
const time = new Date(date); // date (optional): a timestamp(ms) or a date time string

// Date static methods
const time = Date.now(); // return the current Date
const time = Date.parse("ISO_8601"); // use with standard ISO 8601
const time = Date.UTC();

// if date is invalid so the console.log will display Invalid Date or NaN
let date = new Date("10:10 20:10:2024");
console.log(date); // Invalid Date
```

### 1.2. Basic Date methods

```javascript
    // it is not necessary to remember all Date methods
    // you just comprehend the concepts of time: FullYear, Month, Date, Day, Hours, Minutes, Seconds, Milliseconds.
    // The methods are getters and setters.
    // Work with UTC, just add UTC keyword on the methods

    const time = new Date(2012, 10, 20, 10, 20, 30, 50); // monthIndex in range [0, 11], dayIndex is range [0, 6]

    // Getters
    console.log(date.getFullYear());
    console.log(date.getMonth());
    console.log(date.getDate());
    console.log(date.getDay());
    console.log(date.getHours());
    console.log(date.getMinutes());
    console.log(date.getSeconds());
    console.log(date.getMilliseconds());

    // Setters
    console.log(date.setFullYear());
    console.log(date.setMonth());
    console.log(date.setDate());
    console.log(date.setHours());
    console.log(date.setMinutes());
    console.log(date.setSeconds());
    console.log(date.setMilliseconds());

    // Work with UTC
    console.log(date.getUTCFullYear());
    console.log(date.setUTCFullYear());

    // Example usage: concatenate date string
    console.log(${date.getDate()}:${date.getMonth()}:${date.getFullYear()});

```

### 1.3. getTime(), getTimezoneOffset()

```javascript
// Usage: getTime() will return timestamp (ms)
// Use to compare two moments of time, or use to store data into Database.
// example: Ask user to enter the time to start and end of an event.
const dateStart = new Date("2024-05-09");
const dateEnd = new Date("2024-04-09");

if (dateEnd > dateStart) {
  console.log("Fetch data successfully!");
} else {
  console.log("The ended time must happen after the started time");
}

// Usage: getTimezoneOffset() return the difference between the standard time zone
```

### 1.4. Convert Date object to string

```javascript
    console.log(new Date().toISOString); // convert date to ISO 8601 string
    console.log(new Date.toLocaleString(locales, options); // convert date to string according to region and options format
```

**Reference**: <a href="https://www.w3schools.com/jsref/jsref_tolocalestring.asp">Locales and options</a>