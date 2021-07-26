# decluttering
This notebook attempts to find potential clutter in the organisation, and send a gentle reminder to the item owners to consider removing the items. 

![image](https://user-images.githubusercontent.com/2769383/126948765-d0770d29-23e7-4f4c-bc24-eb51ebd32663.png)


As an ArcGIS administrator, I don't want to stifle content creation amongst my Web GIS users, but I do want to gently remind them to clear out items that are no longer being used. 

This notebook will detect and notify users about items that are:

* Not getting recent views
* Larger filesizes
* Are old

It writes the results into a feature table that can be used for reporting purposes if required.
![image](https://user-images.githubusercontent.com/2769383/126941980-25d64e35-6820-4a92-a638-ba7ea529ee62.png)

## Setup

* Download the notebook
* Login to a your ArcGIS Online account (recommend testing in a free **developer plan** or staging subscription first)
* Content section --> New Item
* Drag and drop the notebook in
* Add some metadata to item
* Create new table in your organisation using this [template](https://esriau.maps.arcgis.com/home/item.html?id=5652d25a937b4caf81e3be82ef8abe30)
* Update the variable shown in cell below 
* Run through the cells

![image](https://user-images.githubusercontent.com/2769383/126948124-937518fb-e039-46bb-9ef8-75bba3e31288.png)


![image](https://user-images.githubusercontent.com/2769383/126859298-11fc1d12-a4b2-4745-9161-0ce711dd21ba.png)

### Schedule for a Monthly Inspection

You can [scheule the notebook](https://doc.arcgis.com/en/arcgis-online/create-maps/prepare-a-notebook-for-automated-execution.htm) to run as a task.

Having this run as a fortnightly or monthly task is usually sufficient for most reporting purposes.

![image](https://user-images.githubusercontent.com/2769383/126923425-4830989c-7696-4e5e-9de4-3ce8d97a76dc.png)
