# chrono_period

![Crates.io](https://img.shields.io/crates/v/chrono_period)
![Docs.rs](https://docs.rs/chrono_period/badge.svg?version=0.1.0)
[![Build Status](https://travis-ci.org/jwir3/chrono_period.svg?branch=master)](https://travis-ci.org/jwir3/chrono_period)
![Maintenance](https://img.shields.io/maintenance/yes/2019)

An add-on for chrono that creates a period for tracking durations that have a specific start date.

## Installation
This is an add-on to [chrono](https://docs.rs/crate/chrono/0.4.10), so you will want to install this in combination with that library. Inside of your `Cargo.toml`, add the following:

```
[dependencies]
chrono = "^0.4.10"
chrono_period = "^0.1.0"
```

## Usage

You can create `NaivePeriod` instances from either two instances of `NaiveDateTime`:

```
let start = NaiveDateTime::new(NaiveDate::from_ymd(2020, 1, 1), NaiveTime::from_hms(0, 0, 0));
let end = NaiveDateTime::new(NaiveDate::from_ymd(2021, 1, 1), NaiveTime::from_hms(0, 0, 0));

let np = NaivePeriod::new(start, end);
```

or from a `NaiveDateTime` and a `Duration`:

```
let start = NaiveDateTime::new(NaiveDate::from_ymd(2020, 1, 1), NaiveTime::from_hms(0, 0, 0));

let np = NaivePeriod::from_start_duration(start, Duration::days(366));
```

Once created, `NaivePeriod`s can be used to intersect with one another:

```
let start = NaiveDateTime::new(NaiveDate::from_ymd(2020, 1, 1), NaiveTime::from_hms(0, 0, 0));

let np1 = NaivePeriod::from_start_duration(start, Duration::days(366));

let end = NaiveDateTime::new(NaiveDate::from_ymd(2021, 1, 1), NaiveTime::from_hms(0, 0, 0));

let other = NaivePeriod::new(start, end);

let intersection = np.get_intersection_with(other);

assert_eq!(np1, intersection.unwrap());
```

## Roadmap

Currently, only time periods without time zones are handled. It would be nice if we also handled intersections of dates/times with offsets.
