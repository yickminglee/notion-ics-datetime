# Notion to ICS with Datetime

__Sync__ your __Notion database events__ (including date time) __to__ your own __Google, Apple, or Outlook calendar__ (via ICS feed). 
*Note: you must deploy this on Railway.*

__The pain point__: Notion database events can be shown in Notion Calendar, but, annoyingly, not in your personal Google/Apple/Outlook calendar. This repo completes the circle: it turns your Notion database into an ICS feed so your events sync to your own calendar apps.


## Features

- Convert a Notion database into an `.ics` feed
- Read and transfer Notion **datetime** values into calendar events
- Subscribe to the feed from calendar apps
- Deploy on Railway

## Good fit for

Any situation where the event time matters, such as:
- Planning your own schedule
- Managing content posting dates
- Tracking bookings or appointments

## Example use case

Plan events in Notion, publish them as an ICS feed, and view them in your normal calendar app with the correct date and time.


## What you need

- A Notion integration token
- A Notion database ID
- A Notion database with a title field
- A Notion database with a date field
- A Railway account


## Configuring

1. Create a new project on Railway
2. Deploy this repo from GitHub
3. Generate a secret key for `ACCESS_TOKEN` in your terminal:
   ```bash
   node -e "require('crypto').randomBytes(48, function(ex, buf) { console.log(buf.toString('base64')) });"
   ```
4. Add your private environment variables (Railway->Variables->):
   - `ACCESS_TOKEN`
   - `NOTION_TOKEN` (see Notion steps below)
5. [Optional] Update `src/lib/config.ts` for your database's properties. See the Notion docs for the [filter schema](https://developers.notion.com/reference/post-database-query#post-database-query-filter).
6. Build and deploy the site!
7. Open your calendar ICS URL:
   
   (i) In Railway, go to **Settings → Networking → Public networking** and open your domain link.
   
   (ii) Add this to the end of the domain link:
      `/<database-id>.ics?secret=<generated-secret>`
      (see Notion steps below for how to get your database ID).
   
9. Subscribe to that ICS URL from your Google, Apple, or Outlook calendar app

### Notion Steps
1. Create a new Notion integration by visiting https://www.notion.so/my-integrations. We only need the "Read content" and "No user information" capabilities. This should be an internal integration.
2. Copy your internal integration token into Railway->Variables->`NOTION_TOKEN`.
3. Share the database(s) you want with the integration by opening your database as a page, going to "Share", and selecting your integration.
4. Save your database's ID by copying the database URL and selecting the part between the slash and the question mark. The ID is 32 characters.

Note: For more information on the Notion steps, see the [Notion docs](https://developers.notion.com/docs/getting-started).

## ☕ Support ☕

I like building small tools that make life a bit simpler. If this project helped you, you can support my work here:

☕ [Buy Me a Coffee](https://buymeacoffee.com/ming.lee) ☕

## Credits

This is an improved fork of [`tctree333/notion-ics`](https://github.com/tctree333/notion-ics), extended for real-world scheduling:
- proper datetime support
- Railway deployment




