# Frequently asked questions

The goal of this document is to provide concise answers to commonly asked questions pertaining to setting up, deploying, and maintaining DRIVER2.0. Many of these topics are covered more in-depth in other sections of the documentation, so please read through the complete set of documentation in order to gain a better understanding of the system.


## Sections
- [**Setup**](#setup)
- [**Deployment**](#deployment)
- [**Environment**](#environment)


## Setup

### Why am I seeing SSL errors when running `curl` commands?
Your version of cURL may not have the right certificate authorities installed. Try passing the `-k` parameter to `curl`.

### How can I make a field searchable?
You can change the field in the schema editor by going to https://[DRIVER2.0 domain]/editor/. Drop down "Incident" on the left side and go to "View Related Content". Then, click the "Edit" button on the group the field belongs to. In there each field has a checkbox for `Filterable/Searchable` that if checked, it will become filterable (if a drop-down field) or searchable (if a text field).

### Why do I see an error fetching gpg key from keyserver while provisioning?
This comes up occasionally and is generally seen as transient issue, i.e., after running the command again, the issue would not show itself.

### Why do I see the JavaScript error: `Cannot read property 'uuid' of undefined`?
This can happen if no Record Type exists with the name configured in: `web_js_record_type_primary_label`. Make sure to update that group_var accordingly.

### Why do I see the JavaScript warnings: `No geographies returned`, `No boundaries returned`, or `No record types returned`?
Geographies, boundaries, and record types need to be configured within the schema editor before the application can be used.


## Deployment

### Where are the Docker images hosted?
Docker images are currently being hosted on `quay.io`.


## Environment

### What is the operating system on which the database server is hosted?
The operating system on all the machines is Ubuntu 18.04 (Linux).

### What database is used within DRIVER2.0?
DRIVER2.0 uses PostgreSQL with the PostGIS extension.

### What is the main language/framework used to build this system?
DRIVER2.0 uses JavaScript, Python, HTML, CSS, and a small amount of Java and R. The front-end UI of the app uses the Angular v8.1.x framework and the back-end uses the Django web framework.

### What is the client-side technology used by DRIVER2.0?
HTML5 (consumed in any modern web browser), a native Android and iOS app.

### What set of basemaps does DRIVER2.0 use?
The basemaps are using Carto. You should see requests to map tiles similar to `https://cartodb-basemaps-b.global.ssl.fastly.net/light_all/5/12/16.png` in your network tab.

### Does DRIVER2.0 have links to or interfaces with other systems?
DRIVER2.0 gathers crash records from its companion Android/iOS applications, which runs on users' Android/iOS smartphones. It also interfaces with OpenWeatherMap and iRAP.  OpenWeatherMap is an API that provides weather information for the crash records. It pulls street information from Open Street Map extracts from GeoFabrik. Pickpoint.io is used for geocoding and reverse geocoding. DRIVER2.0 grabs street-level images from Mapillary to display to the user. DRIVER2.0 uses a basemap tile service from Carto.
The iRAP API provides the star rating, road features and the iRAP toolkit. This information is generally used to pull the street information for the specific datasets assigned to the particular user.

### Does DRIVER2.0 have News Feeds or Widgets (e.g. RSS, Twitter, Atom, etc.)?
No, there isn't any news feed integration.

### Does DRIVER2.0 have any type of authentication or access control mechanisms that will be present when the site is live and in production?
The site requires authentication to use. It offers two methods of authentication. One is username/password authentication. The second is Single Sign On (SSO) that can be accessed if the user has a Google account. The SSO is achieved via the OAuth protocol. The site does not utilize 2FA/MFA. Once authentication has been achieved, the user receives a token that is used to authenticate each request to the site's API.

### What APIs does the Android/iOS app require access to?
The DRIVER2.0 Android/iOS app needs access to the camera, Location and Notification API.
