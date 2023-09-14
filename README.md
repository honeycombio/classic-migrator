# Honeycomb Classic-Migrator

The Honeycomb Classic Migrator is a tool designed to streamline the process of migrating your features and configurations (boards, derived columns, triggers, etc) from [Honeycomb Classic](https://docs.honeycomb.io/honeycomb-classic/) to our modern [Environments & Services](https://changelog.honeycomb.io/preview-new-environments-and-services-functionality-in-honeycomb!-227356) data model.

Classic Migrator is distributed as a single binary (built by Go), which serves a web interface to the user, guiding them through all the necessary migration steps. It fetches all needed dependencies and places them in the working dir (specified on the command line as `--working-dir`).

## Running the Classic-Migrator

### Downloading:
Grab the latest release from the [Releases section](https://github.com/honeycombio/classic-migrator/releases) of this repo

On Mac and Linux, remember to `chmod +x classic-migrator` after downloading

### Running:
```
./classic-migrator --listen-on localhost:8000 --working-dir ~/migrations/

To get started, visit http://localhost:8000 in your browser.
```

### Demo Video
(Click the unmute icon to hear the voice track)

https://user-images.githubusercontent.com/1616328/224799312-ea835129-6c22-49e3-88a0-020e399b21c2.mp4

### debug mode:
set `ENV=development` before running the classic-migrator command

### Performing the migration:

If not already done, [create a new environment](https://docs.honeycomb.io/honeycomb-classic/migration/#create-a-new-environment) (the migration destination).

Next, [create API keys](https://docs.honeycomb.io/working-with-your-data/settings/api-keys/) for both the classic and new environments with the following permissions: Send Events, Create Datasets, Manage Queries and Columns, Manage Public Boards, Manage SLOs, Manage Triggers, Manage Recipients.

Now visit http://localhost:8000 in your browser and you will be asked to enter in the API keys created previously. Click 'Let's get started!' and on the next page select the Classic dataset you want to migrate.

After selecting a dataset the migrator will import all resources, identify & fix (when possible) any that cannot be migrated, and present a list of SLOs and Triggers. SLOs and Triggers require mapping to a specific dataset in the new environment.

To decide which dataset to select, first check if any of these are no longer needed/in use and could be ignored. Next, consider if any of your Triggers or SLOs could be reworked to look at a gateway service or other common point of infrastructure. For the remainder, you can mouse over 'Open Query' to see the query in question. If a service name is defined, choose that service name as the destination dataset. Should you need to map a Trigger or SLO to multiple datasets, simply select one on this screen and after the migration on the next step is complete, you can edit the resources.tf file and make as many copies of the resources as needed, up to your team's limits.

Once all Triggers and SLOs have been mapped to a destination dataset, click 'Migrate this dataset!' and the terraform will run. Should any errors arise, review the troubleshooting steps on screen and edit the resources.tf file as needed. If you have any questions, please reach out to https://support.honeycomb.io/ or our [Pollinators Community Slack](https://join.slack.com/t/honeycombpollinators/shared_invite/zt-xqexg936-dckd0l29wdE3WLmUs8Qvpg) server.

## Troubleshooting

### macOS unidentified developer error

If you try to run the classic-migrator on macOS and receive the error:
```
"classic-migrator" can't be opened because it is from an unidentified developer.
```

Go to Settings -> Privacy & Security  and scroll down to the Security "Allow applications downloaded from" section.

Typically, macOS will give you a chance to exempt individual apps, like so:
![Alt text](<macos-ventura-allow-unidentified.png>)

If that doesn't work, check out [these instructions](https://osxdaily.com/2022/11/17/allow-apps-downloaded-open-anywhere-macos/)
