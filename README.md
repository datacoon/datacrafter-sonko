# What is it?

Database and code of social NGOs in Russia from https://data.economy.gov.ru portal and enriched with OpenNGO.ru data about current status and organization classification.

This dataset could be reused for further data enrichment, data analysis and vizualization.

# How to use

## Requirements

* Local MongoDB instance
* Python 3.6+
* [datacrafter](github.com/apicrafter/datacrafter) ETL tool installed
* mongorestore tool in PATH


## Quick use

Just take database from `output/dump/openngo/sonko_fin.bson.gz` and load it into local MongoDB using `mongorestore`

## Collect data
If you would like to collect data use [datacrafter](github.com/apicrafter/datacrafter) tool to collect data from data.economy.gov.ru
Command ```datacrafter run```

## Process data

**Load raw data into MongoDB**
Uses output/data.bson file and loads it with mongorestore
```
cd code
python3 process.py loadraw
```

Creates db **openngo** and collection **sonko_raw**

**Create staging DB**
Processes raw data in MongoDB and generates staging collection 
```
cd code
python3 process.py stage
```

Creates db **openngo** and collection **sonko_stg**

**Enrich data**
Enriches data with data from NGO organizations profiles from openngo.ru
_Warning - for internal usage only. Prepared dataset already provided. if you would like to have this data, ask for API access or data dump here ivan@begtin.tech._

```
cd code
python3 process.py enrich
```

Updates collection **sonko_stg**

# Data schema

## Final dataset (sonko_fin)

```
{
  "_id": {
    "type": "string"
  },
  "inn": {
    "type": "string"
  },
  "fullname": {
    "type": "string"
  },
  "shortname": {
    "type": "string"
  },
  "ogrn": {
    "type": "string"
  },
  "records": {
    "type": "array",
    "subtype": "dict",
    "schema": {
      "_id": {
        "type": "string"
      },
      "inn": {
        "type": "string"
      },
      "fullname": {
        "type": "string"
      },
      "shortname": {
        "type": "string"
      },
      "regaddr": {
        "type": "string"
      },
      "ogrn": {
        "type": "string"
      },
      "orgform": {
        "type": "string"
      },
      "okved": {
        "type": "string"
      },
      "sonko_status": {
        "type": "string"
      },
      "ngo_status": {
        "type": "string"
      },
      "inclusion_reason": {
        "type": "string"
      },
      "supporter_name": {
        "type": "string"
      },
      "date_support": {
        "type": "datetime"
      },
      "date_inclusion": {
        "type": "datetime"
      }
    }
  },
  "egrulStatus": {
    "type": "string"
  },
  "tags": {
    "type": "array",
    "subtype": "string"
  },
  "orglists": {
    "type": "array",
    "subtype": "dict",
    "schema": {
      "id": {
        "type": "string"
      },
      "name": {
        "type": "string"
      },
      "website": {
        "type": "string"
      }
    }
  },
  "regionCode": {
    "type": "string"
  },
  "regionName": {
    "type": "string"
  },
  "minjustStatus": {
    "type": "string"
  }
}
```

## Original raw data (sonko_raw)

```
{
  "inn": {
    "type": "string"
  },
  "fullname": {
    "type": "string"
  },
  "shortname": {
    "type": "string"
  },
  "regaddr": {
    "type": "string"
  },
  "ogrn": {
    "type": "string"
  },
  "orgform": {
    "type": "string"
  },
  "okved": {
    "type": "string"
  },
  "sonko_status": {
    "type": "string"
  },
  "ngo_status": {
    "type": "string"
  },
  "inclusion_reason": {
    "type": "string"
  },
  "supporter_name": {
    "type": "string"
  },
  "date_support": {
    "type": "string"
  },
  "date_inclusion": {
    "type": "datetime"
  }
}
```


# Contacts

Write issue [here](https://github.com/datacoon/datacrafter-sonko/issues) or write ivan@begtin.tech. Please introduce yourself and your goals.
