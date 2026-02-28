# Decluttering Notebook
Identify stale content in your ArcGIS Online organisation and send polite, automated reminders to item owners to consider cleaning up.

![image](https://user-images.githubusercontent.com/2769383/126948765-d0770d29-23e7-4f4c-bc24-eb51ebd32663.png)


## Overview

A healthy ArcGIS Online organisation creates a lot of content. Over time, older items accumulate that are no longer actively used but continue to consume storage credits. This notebook helps admins manage that problem without being heavy-handed — it identifies stale items and nudges owners to take action, rather than deleting anything automatically.

As an ArcGIS administrator, I don't want to stifle content creation amongst my Web GIS users, but I do want to gently remind them to clear out items that are no longer being used. 

This notebook will detect and notify users about items that are:

* Not getting recent views
* Larger filesizes
* Are old

Results are written to a Hosted Table in your org for reporting and dashboarding. A public-facing dashboard showing the stale items list is a surprisingly effective way to encourage users to self-manage — no-one wants to appear on the list.

![image](https://user-images.githubusercontent.com/2769383/126949487-1b24d05c-f136-444f-845b-99efe6953197.png)


![image](https://user-images.githubusercontent.com/2769383/126941980-25d64e35-6820-4a92-a638-ba7ea529ee62.png)



## Setup

> ⚠️ **Test first.** Run this notebook against a free [ArcGIS Developer Plan](https://developers.arcgis.com/sign-up/) or a staging subscription before using it in production.

### 1. Create the Hosted Table

The notebook writes results to a Hosted Table. Create one in your org and do NOT make it public.  You can remove email if you do not want this information recorded.  This is to support other workflows where you might want to send emails or work with notification in MS Teams via a bot.

The table requires the following fields:

| Field | Type | Purpose |
|---|---|---|
| `id` | String | ArcGIS item ID |
| `title` | String | Item title |
| `owner` | String | Username |
| `FirstName` | String | Owner's first name (used in notification comment) |
| `email` | String | Owner's email address |
| `disabled` | String | Whether the owner account is disabled (`"0"` / `"1"`) |
| `access` | String | Item sharing level |
| `size_mb` | Double | Item size in MB |
| `numViews60d` | Integer | Views in last 60 days |
| `ReminderSent` | Date | Timestamp of notification — `NULL` means not yet notified |

### 2. Upload the notebook

- Log in to your ArcGIS Online account
- Go to **Content → New Item**
- Drag and drop `declutter.ipynb` into the upload dialog
- Add metadata to the item

Alternatively you can run this notebook from importing it into ArcGIS Pro or VS Code, but then you can't later schedule it to run.

### 3. Configure

Open the notebook and update **Cell 2** — this is the only cell you need to edit before running:

```python
# STALE ITEM THRESHOLDS
views    = 10   # fewer than this many views in the last 60 days
size_mb  = 5    # larger than this many MB
age_days = 40   # older than this many days

# HOSTED TABLE
table_item = 'YOUR_TABLE_ITEM_ID_HERE'  # replace with your item ID

# NOTIFICATION SETTINGS
NOTIFICATION_PREFIX     = '⚠️ AUTOMATED NOTIFICATION'  # do not change after first run
SLEEP_BETWEEN_COMMENTS  = 15  # seconds between comments — do not set below 12
```
> ⚠️ **Do not change `NOTIFICATION_PREFIX` after your first run.** The notebook uses this string to detect previously notified items. Changing it will cause all items to be treated as new and owners will receive duplicate notifications.

### 4. Run the notebook

The notebook is structured as a linear flow. Run each cell in order:

| Cell | What it does |
|---|---|
| 1 | Connect to GIS |
| 2 | Set configuration |
| 3 | Search for all Hosted Feature Services |
| 4 | Scan items and apply stale filters |
| 5 | Preview results as a DataFrame |
| 6 | Write results to the Hosted Table |
| 7 | Return the table item |
| 8 | Query items pending notification |
| 9 | Define `check_comments()` helper |
| 10 | **Preview** notifications — review who will be contacted before proceeding |
| 11 | **Send** notifications — only run once satisfied with the preview |

![image](https://user-images.githubusercontent.com/2769383/126948124-937518fb-e039-46bb-9ef8-75bba3e31288.png)


![image](https://user-images.githubusercontent.com/2769383/126859298-11fc1d12-a4b2-4745-9161-0ce711dd21ba.png)

### Schedule for a Monthly Inspection

You can [scheule the notebook](https://doc.arcgis.com/en/arcgis-online/create-maps/prepare-a-notebook-for-automated-execution.htm) to run as a task.

Having this run as a fortnightly or monthly task is usually sufficient for most reporting purposes.

![image](https://user-images.githubusercontent.com/2769383/126923425-4830989c-7696-4e5e-9de4-3ce8d97a76dc.png)
