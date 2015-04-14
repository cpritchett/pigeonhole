# Pigeonhole

Pigeonhole is an alert analysis and categorisation tool. It takes data from PagerDuty and generates graphs based on this data over a configurable time period.

At present it offers a graph of alert frequency, but we're also looking to and analysis of acknowledgement and resolution times as well as breakdowns over day and time.

## Installation

Pigeonhole requires the following:

  - InfluxDB
  - Ruby 2.1.5 (and rbenv, or your preferred ruby management tool)

After these have been installed, copy the config.toml.example file to config.toml, and update it with your details.

## Usage

There are three parts to Pigeonhole:

### Import from PagerDuty

Pigeonhole will pull all recent events from your PagerDuty account and import them.

```
➤ ./bin/import_from_pd --help
Usage: import_from_pd [options] [start_date] [finish_date]

Takes an optional start and an optional finish date in the form of
'YYYY-MM-DD' or 'YYYY-MM-DDTHH:MM:SS+10:00' and imports all PagerDuty incidents
within those dates into InfluxDB. If no start date is specified, it will
default to today, 00:00:00h. If no finish date is specified it will use now as
finish date.

Options:
    -h, --help                       Show command line help
        --log-level LEVEL            Set the logging level
                                     (debug|info|warn|error|fatal)
                                     (Default: info)
```

### Web UI
After this is been completed as you can load up the pigeonhole interface by running:

```
bundle exec shotgun
```

Pigeonhole is now able to be viewed at http://127.0.0.1:9393/

### Alert Categorisation Reminder

To aid in alert categorisation, Pigeonhole includes a script to remind recent people on call to categorise the alerts they received.  This can be run using:

```
➤ ./bin/email_reminder_to_oncall --help
Usage: email_reminder_to_oncall [oncall_date]

Takes an optional date (defaults to today) in the form of 'YYYY-MM-DD' and
sends an email reminder to whoever was on call.
    -h, --help                       Show command line help
```

## Screenshots

### Categorisation mode

![Categorisation Mode](screenshots/categorisation.png?raw=true "Categorisation Mode")

### Breakdown mode

![Breakdown Mode](screenshots/breakdown.png?raw=true "Breakdown Mode")

We hope you find this useful!