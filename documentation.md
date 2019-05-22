# Creating and hosting Leaflet maps with qgis2web and GitHub

## Getting started
### Difficulty: Medium
This tutorial requires basic knowledge of Google products (e.g., searching) and working with spreadsheets (e.g., adding and copying functions). No prior experience with GIS or Javascript is necessary. Some familiarity with HTML and HTML documents is helpful.

### Download dependencies
This tutorial was made using Mac iOS High Sierra v 10.13.6. The following software is used and should be installed before beginning:

- QGIS3--See the appendix for assistance installing on a Mac
- GitHub account
- GitHub Desktop
- Atom text editor
- Firefox and Chrome web browsers
- Google account (i.e., Gmail account)
- Google Sheets or Excel
- Terminal
- WordPress Business account with iFrame plugin

## Create a GitHub repository
1. Go to github.com and login. Create a new account if needed.

2. Next to **Repositories** click **New** to create a new repository. Provide a name at a minimum. Fill out the information. A license is not required, but I Like to use [Creative Commons](https://creativecommons.org/)

  ![alt text](images/newRepo.png "Create repository")

3. Click **Set up in Desktop**. If a window appears in the browser asking how to open it, choose the option **Open GitHub Desktop.app**.

  ![alt text](images/setUpDesktop.png "Set up in desktop")

4. Make sure the local desktop path looks correct, i.e., somewhere you will remember, and click **clone**.

## List places and draft text
While I am travelling, I make sure to write down the names of the places that I visit: restaurants, sites, etc.

1. List the places to display on a map in spreadsheet. This documentation shows Google Sheets. If using an Excel or Numbers file, this should be saved in the git repository created in the previous section.

2. Once the places are listed, in the next column write the content to be displayed on the map when the place is clicked in the final map. This text will also be used in the text description to show below the map.

## Image processing
### Add images to git repository and resize images
1. Load photos to computer. I take photos with an iPhone, so I use AirDrop.

2. If not done previously, create a new folder in the git repository called images.

3. Copy photos into git repository file titled images. Make sure to **COPY** the images or have a backup because these images will be resized.

4. If desired, rename the photos to something more descriptive and memorable.

5. Open the Terminal. If you are not sure where Terminal is, type Terminal into Mac's spotlight.

  ![alt text](images/terminal.png "Terminal in Spotlight")

6. Change the directory using the command `cd` to the git repository with the images. For example:

```
cd git
cd 2019_oslo
cd images
```
  Or use a relative path like:
```
cd git/2019_oslo/images
```
7. Once Terminal shows that it is in the directory for the images, use the following code to resize the images to 300 pixels, or the desired resize:

```
sips -Z 300 *.jpg
```
  In the above code the **300 is the pixel width**--the height is auto-scaled. The * (asterisk) represents choosing **all files** with the file type .jpg. **The code above is case sensitive.** Meaning, sometimes I need to run this twice because the file type of some images is **.JPG** and not **.jpg**. This also works for .png, .tiff, etc. I do not suggest using anything larger than 300 pixels in the leaflet popup--these maps are not exactly the best platform for showcasing high-quality images.

8. Open GitHub Desktop

  - If not already selected, select the project repository.
  - Notice the relative path for all images added are listed in Changes.
  - I like to delete or set up a .gitignore for the .DS_Store file because it is not necessary. Right click the .DS_Store file for either of these options.


9. At the bottom of the column on the left, type in a summary such as initial commit. If working with others on this project, add a more detailed description.

10. Click **Commit to master**.

  ![alt text](images/initialCommit.png "initial commit to repository")

11. This is probably the first thing added to the repository, so click **Publish branch** at the top of the window. Depending on how many images, this can take a few moments. If it is taking a very long time, it may be because the images were not resized.

12. Go to GitHub.com and view the repository.

13. Click the folder for images.

14. Click on an individual image link in the folder.

15. Right click the image, and choose copy image address.

  ![alt text](images/copyPath.png "Copy image path")


16. Open the spreadsheet with the place names and descriptions.

17. Paste the image link into an empty column in the row the place described. If using a new spreadsheet, place it  **A1**.

  ![alt text](images/pathSheets.png "Paste file path")

18. Keep copying and pasting image addresses in a down the column or next to any place with an image for all remaining images. There are many ways to get the image links into the spreadsheet. For example, you can also change the image name in the link, or if there are more than 20, finding an automated way to capture addresses may be helpful.

19. In an empty cell in the rows with images, create alt text to be read by screen readers or to display when the image does not appear.

  ![alt text](images/altText.png "Create alt text column")

20. In the next empty cell in the row type `=CONCATENATE`

21. Within the parentheses type: ``"<img src=+,A1,"+,"alt=+,B1,"+>"``

22. Copy this formula down the column.

23. Copy the column and paste as values in the next empty column. Use command + shift + v to paste as values, or right click/control click and choose Paste Special>Paste Values Only

24. Use find and replace for the + or special character used as a placeholder for the quotation mark in the concatenate function.
  - Press command or ctrl + F
  - Press the three stacked dots at the right of the window for more options.
  - Type + in Find and " in Replace with. Then, press Done.

  ![alt text](images/findReplace.png "Use Find and Replace for special characters")

  ![alt text](images/findReplaceComplete.png "Quotations should replace plus sign or special characters")

## Create geospatial data with MyMaps

### Add places
I start by creating a map with mymaps.google.com to search and either manually pin or search for the places. Sometimes the places I visit might not have a precise address or indexed location, so I really like being able to see the location with the imagery.

However, if you have more than 20 places to map that are likely to be on Google under known place names, use Geocode by Awesome Table on the sheet used in the previous section, download as .csv, and either add it to MyMaps to check the geocoding or add it directly to QGIS. If anything appears incorrectly in MyMaps, manually move any that are in the incorrect place.

1. Go to [mymaps.google.com](https://mymaps.google.com). If you do not have a Google account, [create one](https://accounts.google.com/SignUp) to save projects.

2. Click the red circle with the plus sign in the bottom right to create a new map.

3. Search for a place traveled in the search bar by typing it in or copying it from the spreadsheet and pressing enter/return or clicking the magnifying glass button.

  ![alt text](images/searchPlace.png "Search for a place")

4. If the place appears in the correct place, click +Add to map in the bottom of the pop up box.
If the place does **not appear**, zoom around the map to try to find the approximate location, and then, click the balloon icon below the search bar to manually add a marker.
  - Repeat either process for all places.
  - Keep all points in one layer.


5. Next to the layer title, which is probably **Untitled layer**, click the three stacked dots and Open data table.

  ![alt text](images/dataTable.png "Open the data table")

6. At this point, it is possible to add new columns and include any text descriptions and data desired.
  - This is when I like to add the text description (in the description column), links, image links, and any other desired content.
  - I usually add the image link in the description, but some may prefer to have it in its own column, especially if every place has an image.
  - When adding image links to the description column, add a manual line break in the cell between the text and link using shift + enter/return. Just using enter/return will select the next cell.
  - To add an image link copy what is from the spreadsheet in the previous sections or create a new one using something like: `<img src="https://github.com/yourname/yourrep/img.jpg" alt="Don't forget to add descriptive alt text">`
  - **Image links will appear as text NOT an image in MyMaps**
  - If preferred, add categories for the places, such as site, lodging, food.
  - To capitalize the column titles, click the column title dropdown and choose Duplicate. In the popup, change the title to the desired word or phrase. **Single words are preferable**.
  - Organizing the data table usually comes down to how you want people to consume your content.

### Export KML
1. To the right of the map title, click the three stacked dots.

2. Choose Export to KML/KMZ.

3. In the pop up, click the radio button for **Export as KML instead of KMZ.**

4. Click Download.

## Working with QGIS
If downloading QGIS3 for the first time, see the appendix for installing on a Mac. It is not a one-click install and has very specific Python requirements.

### Installing QGIS Plugins
1. Open QGIS.

2. Click **Plugins** from the top menu.

3. Click manage and install plugins.

4. Search for: **qgis2web**.

5. Below the plugin description, click **Install Plugin**.

6. In the search results, make sure the box next to it is checked so that it appears.

7. Search for **QuickMapServices**, and click **Install Plugin**. Make sure the box next to it is checked, too.

8. Close the plugins window.

9. From the **top menu**, click **Web**. Qgis2Web and QuickMapServices should both appear there. If not, quit QGIS and reopen it. If it still does not appear, go back to the manage and install plugins window and check that these are listed in Installed Plugins. If the plugins are listed there, make sure the box to the left of the plugin is checked.

### Create Projected GeoJSON
Now, the data from MyMaps needs to be reprojected to match the OpenStreetMap projection: EPSG 3857.
1. Open QGIS if it was closed after the last section.

2. Drag the downloaded KML into the layers panel. If the layers panel is not open, from the top menu click View>Panels>Layers.

3. Open Processing toolbox. Do this by clicking the gear icon, of from the top menu, View>Panels>Processing Toolbox.

4. Search for reproject.

5. Double click reproject layer.

6. For the parameters in the window that appears:
  - Input layer should be the kml from MyMaps. Search for it if necessary
  - The Target CRS is EPSG:3857. If it is not in the dropdown, click the globe icon and search 3857. This projection appears under Projected Coordinate Systems>Mercator>WGS 84 / Pseudo-Mercator, Authority ID EPSG:3857.
  - For Reprojected, click the three dots at the end, and choose Save to File.
  - Change the output file type to .geojson, give it a name, and choose the Git repository for this project as the save path.


7. Export the layer.

8. Remove all layers from the map.

9. Add the reprojected layer that is in the git repository.

10. Click Web>QuickMapServices>OpenStreetMap>OSMStandard.

11. Do the points (or whatever data used) look correct on top of the OpenStreetMap basemap?

### Edit the data
KML files come with a lot of extra columns, and this carried over to the geojson. Let's fix that and more!

1. Make sure QGIS is open and the reprojected geojson is in the Layers Panel.

2. Right click the layer, and choose open attribute table.

3. Click the pencil icon in the top left of the attribute table.

4. Click the icon for removing a column.
**Note**: Deleting a column is permanent. You may want to copy the geojson if this is your first time just in case.

5. In the window that appears, click the following columns to select them for deletion:

6. Click remove.

7. Click the floppy disc icon to save edits.

8. While in the attribute table, make any other content edits.

9. Click the pencil icon in the top left again when finished. Make sure to save edits.

### Styling the map
You may wish to style the points or categorize the data on the map. However, you can also leave the default point marker and change it to a leaflet style, which is demonstrated in a later step.

### Using qgis2web to export Leaflet code

### Editing qgis2web index.html file
- Adding responsive stuff
- Adding height/width for images
- editing anything else in line such as colors, changing icon
- Adding custom start view point
- Adding Google Hybrid (imagery AND streets) as basemap
- Do ctrl + F for **http**. Change any http in a web address to https.

### Push to GitHub


### Create gh-pages


### Integrating with a website
Iframe html tags <iframe> do not seem to be compatible with most instances of WordPress as of May 2019. The best reason I could find was "due to security reasons"

Iframe html tags work with some university institutional instances such as NYU Web Publishing (wp.nyu.edu).

#### WordPress plugin: iframe
If you want to integrate with a WordPress, a **business plan** is required to access the iframe plugin.

Create a new page or post,

If serving up your own website, an iframe is probably fine, but if you are hosting your own website, you might be way ahead of this tutorial.

### Making map text description
