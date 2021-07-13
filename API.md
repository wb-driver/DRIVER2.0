# API Documentation
## Overview
DRIVER is a flexible app for storing crash data and related information. DRIVER provides a robust REST API for querying its data. This document describes how to interact with the DRIVER API.

## Table of Contents
- [**Resource Types**](#resource-types)
- [**Authentication**](#authentication)
- [**Requests and Responses**](#requests-and-responses)
- [**Record Types**](#record-types)
- [**Record Schemas**](#record-schemas)
- [**Records**](#records)
- [**Boundaries**](#boundaries)
- [**Boundary Polygons**](#boundary-polygons)
- [**Black Spot Sets**](#black-spot-sets)
- [**Black Spots**](#black-spots)
- [**Registration**](#registration)
- [**My Account**](#my-account)
- [**User Permissions**](#user-permissions) 
- [**Country Details**](#country-details)
- [**Language Details**](#language-details)
- [**Group Details**](#group-details)
- [**Weather Info**](#weather-info)
- [**Crash Type**](#crash-type)
- [**Bulk Upload**](#bulk-upload)
- [**Crash Factor Matrix**](#crash-factor-matrix)

## Resource Types

The following resources are made available via the API:

* Records

    * This contains crash data.

* Record Types

    * The DRIVER system stores other information besides crash data; Record Types are used to group together Records which store a particular type of information.

* Record Schemas

    * Defines exactly what fields may be expected on a given Record.

* Boundaries

    * Groupings of subdivisions of an area. For example, provinces or states within a country where DRIVER is being operated.

* Boundary Polygons

    * Provides a GeoJSON representation of the polygons present in each Boundary.

* Black Spots Sets

    * Groupings of Black Spots, which represent areas where crashes are predicted to occur with higher-than-usual frequency.

* Black Spot

    * Information about a particular Black Spot.

Note : there are other resource types available but they are used primarily for internal purposes; a complete list of resource types is available by sending an authenticated GET request to /api/ (see below).

## Authentication

In order to interact with the DRIVER API you will need a user account. This can be given to you as a username and password by an administrator, or you can use your Google account to sign up.

Once you have a user account, you will need to obtain an API token.

**Developer Tools**

One way to retrieve your API token is by using the developer tools panel.  Once you have access to the system, open up the panel by hitting F12.  Refresh the page and view the network tab of developer tools.  Look for a request to one of the application’s API endpoints (e.g. to the `/api/boundaries/` endpoint).  In the request headers look for the `Authorization` key-value pair.  This contains your API token, listed as `Token [token value]`.

**Username / Password**

To gain a token using your username / password, you will need to send a POST request to /api-token-auth/ with a payload of the following form:
```
{

    "password": "your-password-here",

    "username": "your-username-here"

}
```
You will then receive a JSON response with the following format:
```
{

    "user": <integer>,

    "token": "token-here"

}
```

`Authorization: Token <token>`

## Requests and Responses

Communication with the API generally follows the principles of RESTful API design. API paths correspond to resources, GET requests are used to retrieve objects, while POST requests are used to create new objects. This pattern is followed in nearly all cases; any exceptions will be noted in the documentation.

Responses from the API are exclusively JSON, unless another format is clearly required (CSV exports, for example).

Endpoint behavior can be configured using query parameters for GET requests, while POST requests require a payload in JSON format.

### Pagination

All API endpoints that return lists of resources are paginated. The pagination takes the following format:
```
{
    "count": 57624,
    "next": "[http://localhost:7000/api/records/?offset=20](http://localhost:7000/api/records/?offset=20)",
    "previous": "[http://localhost:7000/api/records/](http://localhost:7000/api/records/)",
    "results": [

        ...
    ]
}
```
In a real response, the domain and port for the next and previous fields will be that of the server responding to the request.

This format applies to the API endpoints below and will not be repeated in the documentation for each individual endpoint.

### JSON-Schema

The DRIVER API makes heavy use of [JSON Schema](http://json-schema.org/) -- it's a good idea to gain familiarity with how JSON Schema works before interacting with the API.

## Record Types

Paths

* List: `/api/recordtypes/`

* Detail: `/api/recordtypes/{uuid}/`

Query parameters

* `active`: Boolean

    * In the UI, Record Types are deactivated rather than deleted entirely. Generally, you will want to limit yourself to active Record Types.

Results fields

* `uuid`: UUID

    * Unique identifier for the RecordType

* `current_schema`: UUID

    * The currently active schema for this RecordType

* `created`: Timestamp

* `modified`: Timestamp

* `label`: String

* `plural_label`: String

* `description`: String

* `active`: Boolean

**Notes**

Because the data schema for a RecordType can be changed by system administrators or programmatically, it is *highly* recommended to use the RecordType API in order to discover the most recent RecordSchema for the RecordType you are interested in before performing further queries. Record Types do not change frequently after initial setup is complete, so knowing the UUID of the Record Type you're interested in will usually be sufficient.

## Record Schemas

Paths

* List: `/api/recordschemas/`

* Detail: `/api/recordschemas/{uuid}/`

Results fields

* `uuid`: UUID

    * Unique identifier for the Record Schema

* `created`: Timestamp

* `modified`: Timestamp

* `version`: Int

    * A sequential number indicating what version of the Record Type's schema this is. Starts at 1.

* `next_version`: UUID

    * Unique identifier of the RecordSchema with the next-highest version number for this schema's Record Type.

    * Null if this is the most recent version

* `record_type`: UUID

    * Unique identifier of this Record Schema's Record Type

* `schema`: Object

    * A JSON Schema object

## Records

**Paths**

* List: `/api/records/`

* Aggregation:

    * `/api/records/stepwise/`

        * Returns a weekly aggregation of the matching Records suitable for constructing a bar or line graph

        * Results are returned with an **array** as the root JSON object. Each element in the array is an object representing the count of Records in a given week of a year. Because weeks often cross the boundary between two years, it is **not** true that the sum of the Record count for all weeks in a year will always be the same as the number of Records in that year. It is also **not** true that a year will always have 52 weeks; years can be assigned up to 54 weeks depending on where each New Year's Day falls. This functionality uses the Postgres EXTRACT function to determine the week and year into which an event falls. Please see [the documentation for EXTRACT](https://www.postgresql.org/docs/9.4/static/functions-datetime.html#FUNCTIONS-DATETIME-EXTRACT) for more information about how this works.

        * Element fields

            * `count`: Int

            * `week`: Int

                * The week number within the year.

            * `year`: Int

                * The year number

    * `/api/records/toddow/`

        * Returns an aggregated table of the matching Records broken out by hour of day (ToD) and Day of Week (DoW).

        * Results are returned with an **array** as the root JSON object. Each element in the array is an object representing a time-of-day/day-of-week pair.

        * Element fields

            * `count`: Int

            * `dow`: Int

                * Starts counting at 1, corresponding to Sunday

            * `tod`: Int

                * Starts counting at 0, corresponding to the hour from 00:00 - 01:00.

    * `/api/records/recent_counts/`

        * Returns an aggregation of the number of matching Records over the past 30, 90, and 365 days.

        * Results fields

            * `month`: Int

            * `quarter`: Int

            * `year`: Int

    * `/api/records/crosstabs/`

        * A more generalized version of the ToD-DoW endpoint: returns an aggregated table of the matching Records broken out along user-configurable dimensions

        * This endpoint accepts all the query parameters accepted by the other aggregation endpoints, but requires additional query parameters and also allows optional additional query parameters.

        * Additional Query Parameters

            * Exactly **one** of the following; determines what each row in the resulting table should be

                * `row_period_type`: ['hour' | 'day' | 'week_day' | 'week' | 'month' | 'year' ]

                    * 'day' corresponds to day-of-month

                * `row_boundary_id`: UUID

                    * Each Polygon within the Boundary (for example, municipal districts within a city boundary) will be a row in the table

                * `row_choices_path`: String

                    * Directs the endpoint to use a schema property which is an enumeration of choices as rows in the table. Only Record Schema properties containing the 'enum' key are valid for this parameter. The path is the object path to the property, with each path component separated by a comma. For example, `&row_choices_path=crashDetails,properties,Collision%20type` would cause the endpoint to search for an enumeration at the following path: `
{
    "crashDetails": {
        "properties": {
            "Collision type": { ... }
        }
    }
}
`
Assuming a properly formatted enumeration is found at the path, each possible enumeration value will correspond to a row in the table.

            * Exactly **one** of the following; these operate identically to the row parameters but determine columns instead:

                * `col_period_type`: ['hour' | 'day' | 'week_day' | 'week' | 'month' | 'year' ]

                * `col_boundary_id`: UUID

                * `col_choices_path`: String

            * The following **optional** query parameter is accepted:

                * `aggregation_boundary`: UUID

                    * Generates a separate **table** for each Polygon in the Boundary. The same Boundary should not be used as a row/column and an aggregation Boundary in the same request.

        * Response format (if a field is listed as type "Array of Objects", then the subfields listed for that field correspond to the fields that each object in the array will have)

            * `row_labels`: Array of Objects

                * `key`: String

                    * Unique key for this row; used to link cell data (see below) to the row / column it belongs in.

                * `label`: Array of Objects

                    * `text`: String

                        * Text of the label. When translate (below) is True, this will be a key corresponding to a term, for example DAY.MONDAY, which is then translated client-side depending on the user's configured interface language.

                    * `translate`: Boolean

                        * Whether to translate this text client-side or display it as-is.

            * `col_labels`: Array

                * `key`: String

                    * See `row_labels`, above

                * `label`: Array

                    * `text`: String

                        * See `row_labels`, above

                    * `translate`: Boolean

                        * See `row_labels`, above

            * `tables`: Array

                * `tablekey`: String

                    * Unique identifier for this table

                * `row_totals`: Object

                    * Each field in this object will correspond to the key of a row_label, above. Values correspond to totals. This dictionary is **sparse**, so if a key is not represented, its value is 0. Example (the keys are UUIDs of polygons):
`
"row_totals": {
"96aeb5ca-d077-49fc-8e4d-ab00f96659f8": 4,
"8e008134-df1e-4cb2-86b0-986164a19a71": 438,
"01ed7d29-ea80-4ecf-a028-8ef8f08a5e54": 847,
"379bcf7d-20cc-467b-8746-a5c84f905871": 78
}
`

                * `data`: Object

                    * Each field in this object corresponds to the key of a row_label, above. Values are objects providing totals for each column within that row, via the column_label key. As with row_totals, values are **sparse**. Example (the row keys are UUIDs of polygons, while the column keys are days of the week):
`"data": {
    "96aeb5ca-d077-49fc-8e4d-ab00f96659f8": {
        "1": 1,
        "2": 1
        "5": 2
    }
}`

                * `table_labels`: Object

                    * Similarly to how `row_labels` and `col_labels` work, each key in this object corresponds to the tablekey of a table.

* Detail: `/api/records/{uuid}/`

**Query Parameters**
All list and aggregation endpoints accept the same query parameters except where noted above.

* `archived`: Boolean

    * Records can be "archived" to denote that they should not be included in lists and calculations. Pass "True" to this parameter to return archived Records only; "False" to return un-archived only. Omitting this parameter returns both types.

* `details_only`: Boolean

    * Every Record is auto-generated with a "<record_type>Details" field which is intended to contain a basic summary of information about the Record. Passing "True" to this parameter will omit any other fields which exist on the Record. This is used on the list view to limit the size of the payload returned when only a summary view is needed.

* `record_type`: UUID

    * Limit the response to Records matching the passed Record Type. This is in theory optional but in practice **mandatory** -- it is very rare that it will be useful to return two different types of Records in a single request. It is usually a better idea to make a separate request for each Record Type.

* `jsonb`: Object

    * Query the data fields of the object and filter on the result.

    * Keys in this object mimic the search paths to filter on a particular object field. However, in place of values, a filter rule definition is used. Example:
`{ "accidentDetails": {
    "Main+cause": {
        "_rule_type": "containment",
        "contains": [
            "Vehicle+defect",
            "Road+defect",
            ["Vehicle+defect"],
            ["Road+defect"]
        ]
    },
    "Num+driver+casualties": {
        "_rule_type": "intrange",
        "min": 1,
        "max": 3
    }
}}`. The query above defines the following two filters:

        * accidentDetails -> "Main cause" == "Vehicle defect" OR accidentDetails -> "Main cause" == "Road defect"

        * accidentDetails -> "Num driver casualties" >= 1 AND accidentDetails -> "Num driver casualties" <= 3

    * There is a third filter rule type available: "containment_multiple". This is used when searching a field of which there can be several on a single record. For example, "People" or "Vehicles". Here's an example:
`{"person":{"Injury":{"_rule_type":"containment_multiple","contains":["Fatal"]}}}`

* `occurred_min`: Timestamp

    * Filter to Records occurring after this date

* `occurred_max`: Timestamp

    * Filter to Records occurring before this date

* `polygon_id`: UUID

    * Filter to Records which occurred within the Polygon identified by the UUID

* `polygon`: GeoJSON

    * Filter to Records which occurred within the bounds of the GeoJSON

* `tilekey`: Boolean, List endpoint **only**

    * Instruct the API that you will want to generate tiles from this set of filtered events later. Subsequent requests to the `/tiles/` endpoint using this tilekey will return tiles of events filtered to these query parameters. The tile server is [Windshaft](https://github.com/CartoDB/Windshaft); documenting its API is beyond the scope of this document, but it is an XYZ tile server that should be fairly straightforward to integrate with a mapping library such as Leaflet or OpenLayers.

List / Detail Results fields

* `uuid`: UUID

    * Unique ID of this Record

* `created`: Timestamp

    * The date this Record was created

* `modified`: Timestamp

    * The date this Record was most recently updated

* `occurred_from`: Timestamp

    * The earliest time at which this Record might have occurred

* `occurred_to`: Timestamp

    * The latest time at which this Record might have occurred

    * All DRIVER Records use identical occurred_from and occurred_to timestamps

* `geom`: GeoJSON

    * Geometry representing point where this Record occurred

* `location_text`: String

    * A description of the location where this Record occurred; this is usually an address.

* `city`: String

* `city_district`: String

* `county`: String

* `neighborhood`: String

* `road`: String

* `state`: String

* `weather`: String

    * Description of the weather conditions when the Record occurred

* `light`: String

    * Description of the lighting conditions when the Record occurred

* `archived`: Boolean

    * A way of hiding records without deleting them completely. True indicates archived.

* `schema`: UUID

    * References the Schema which was used to create this Record.

* `data`: Object

    * A JSON object representing the data associated with this Record. It is always true that the object stored in "data" conforms to the RecordSchema referenced by the "schema" UUID.

## Boundaries

Paths

* List: `/api/boundaries/`

* Detail: `/api/boundaries/{uuid}/`

Results fields:

* `uuid`: UUID

* `label`: String

    * Label of this Boundary, for display

* `color`: String

    * Rendering color preference for this Boundary

* `display_field`: String

    * Which field of the imported Shapefile to use for display

* `data_fields`: Array

    * List of the names of the fields contained in the imported Shapefile

* `errors`: Array

    * A possible list of errors importing the Shapefile.

* `created`: Timestamp

* `modified`: Timestamp

* `status`: String

    * Import status of Shapefile

* `source_file`: String

    * URI to the Shapefile that was originally used to generate this Boundary.

**Notes**

Creating a new Boundary and its Polygons correctly is a two-step process.

1. POST to `/api/boundaries/` with a zipped Shapefile attached; you will need to include the label as form-data. You will (hopefully) receive a 201 response which contains a fully-fledged Boundary object, including a list of available data fields in `data_fields`.

2. The response from the previous request will have a blank `display_field`. Select one of the fields in `data_fields` and make a PATCH request to `/api/boundaries/{uuid}/` with that value in `display_field`. You are now ready to use this Boundary and its associated Boundary Polygons.

## Boundary Polygons

Paths

* List: `/api/boundarypolygons/`

* Detail: `/api/boundarypolygons/{uuid}/`

Results fields:

* `uuid`: UUID

* `data`: Object

    * Each key in this Object will correspond to one of the data_fields in the parent Boundary, and will store the value for that field for this Polygon

* `created`: Timestamp

* `modified`: Timestamp

* `boundary`: UUID

    * ID of the parent Boundary for this Polygon.

* `bbox`: Array

    * Minimum bounding box containing this Polygon's geometry, as an Array of lat/lon points

    * Optional (see nogeom parameter, below)

* `geometry`: GeoJSON

    * GeoJSON representation of this Polygon

    * Optional (see nogeom parameter, below)

Query Parameters:

* `boundary`: UUID

    * Filter to Polygons associated with this parent Boundary

* `nogeom`

    * When passed with any value, causes the geometry field to be replaced with a bbox field. This reduces the response size and is sufficient for many purposes.

## Black Spot Sets

Paths

* List: `/api/blackspotsets/`

* Detail: `/api/blackspotsets/{uuid}/`

Results fields

* `uuid`: UUID

* `created`: Timestamp

* `modified`: Timestamp

* `effective_start`: Timestamp

    * Black Spot Sets are predictive and are generated automatically by DRIVER once configured. A Black Spot Set is effective from the time it is generated until it is superseded by a newer Black Spot Set. The effective_start and effective_end (below) fields determine whether a Black Spot Set is effective at a particular date / time.

* `effective_end`: Timestamp

    * Counterpart to effective_start (above). Null if this Black Spot Set is the newest available.

* `record_type`: UUID

    * The Record Type which this Black Spot Set predicts.

Query Parameters

* `effective_at`: Timestamp

    * Only return Black Spot Sets which are effective at the given time.

* `record_type`: UUID

**Notes**

## Black Spots

Paths

* List: `/api/blackspots/`

* Detail: `/api/blackspots/{uuid}/`

Results fields

* `uuid`: UUID

* `created`: Timestamp

* `modified`: Timestamp

* `severity_score`: Float

    * How severe this Black Spot is predicted to be.

* `num_records`: Int

    * The number of Records which contributed to this Black Spot's designation

* `num_severe`: Int

    * The number of severe Records which contributed to this Black Spot's designation

* `black_spot_set`: UUID

* `geom`: GeoJSON

    * The area which this Black Spot encompasses

Query Parameters

* `black_spot_set`: UUID

    * Only return Black Spots associated with this Black Spot Set.
  
## Registration

* List: `/auth-api/adv-registration/`

Query Parameters

* `groups`: Int

* `limit`: Int
  
* `offset`: Int

* `user`: Str


* To create new user account make a POST request to `/api/registration/` with below data params

* `username`: Str
  
* `password`: Str
  
* `first_name`: Str
  
* `last_name`: Str
  
* `email`: Str
  
* `groups`: List
  
* `is_staff`: Boolean

* Results fields

* `groupdetail`: List
  
* `token`: Int
  
* `id`: Int
  
* `first_name`: Str
  
* `last_name`: Str
  
* `username`: Str
  
* `groups`: List
  
* `email`: Email
  
* `date_joined`: DateTime
  
* `is_staff`: Boolean
  
* `is_superuser`: Boolean


* To storing additional user details make a POST request to `/auth-api/adv-registration/` after success response of 
  `/api/registration/` API and pass id returned by `/api/registration/` API as a `user` data param to 
  `/auth-api/adv-registration/`

* `username`: Str

* `password`: Str

* `first_name`: Str

* `last_name`: Str

* `email`: Str

* `groups`: List

* `geography`: UUID

* `is_staff`: Boolean

* `user`: Int


Results Fields

* `id`: Int
  
* `first_name`: Str
  
* `last_name`: Str
  
* `email`: Str
  
* `username`: Str
  
* `geography`: Str
  
* `reg`: List
  
* `city`: List
  
* `org`: List
  
* `groups`: List
  
* `is_active`: Boolean
  
* `date_joined`: DateTime
  
* `updated_on`: DateTime
  
* `user`: Int
  
* `is_role_requested`: Str
  
* `mobile_no`: null
  
* `is_staff`: Boolean
  
* `is_superuser`: Boolean
  
* `is_analyst`: Boolean
  
* `is_tech_analyst`: Boolean
  
* `google_user`: Boolean

## My Account
* To get the user details make a GET request to `/auth-api/user-info/2/` 

Results Fields

* `groupdetail`: List

* `token`: UUID

* `id`: Id

* `first_name`: Str

* `last_name`: Str

* `username`: Str

* `email`: Email

* `groups`: List

* `is_staff`: Boolean

* `is_superuser`: Boolean

* `is_active`: Boolean

* `date_joined`: DateTime

## User Permissions

* To get permissions of a user make a POST request to `/api/get-group-permissions/` with List of codenames and user id

* `codename`: List,
* `user`: Int

Results Fields

* `codename`: Str,
* `status`: Boolean

## Country Details

* To add a country make a POST request to `/api/country-info/` with the following data parameters

* `country_code`: Str

* `country_name`: Str

* `latitude`: Float

* `longitude`: Float

* To get list of countries make a GET request to `/api/country-info/`

Query parameters

* `archived` : Boolean

* Result Fields

* `id`: Int

* `country_code`: Str

* `country_name`: Str

* `archived`: Boolean

* `latitude`: Float

* `longitude`: Float

## Language Details

* To add language make a POST request to `/api/language-details/` with the following data parameters

* `label`: Str

* `upload_for`: Str

* `language_code`: Str

* `csv_f`: application/vnd.ms-excel;base64

* `default_for_user_panel`: Boolean

* `default_for_admin_panel`: Boolean

* `archive`: Boolean


* To get list of languages make a GET request to `/api/language-details/` which will return al of the languages

Query params

* `archive` : Boolean

* Results fields

* `id`: Int

* `label`: Str

* `csv_file`: Str

* `json_file`: Str

* `language_code`: Str

* `upload_for`: Str

* `default_for_user_panel`: Boolean

* `default_for_admin_panel`: Boolean

* `archive`: Boolean

* `created_date`: DateTime

* `updated_date`: DateTime


* To get details of a perticular language make GET request to `/api/language-details/{{IDD}}/` pass id as a query params

* Result fields

* `id`: Int

* `label`: Str

* `csv_file`: Str

* `json_file`: Str

* `language_code`: Str

* `upload_for`: Str

* `default_for_user_panel`: Boolean

* `default_for_admin_panel`: Boolean

* `archive`: Boolean

* `created_date`: DateTime

* `updated_date`: DateTime


* To update details of a language object make a PUT request to `/api/language-details/{{ID}}/` pass id of the object you
  want to update
  

* To get translated text make a GET request to `/api/lang-json/{{lang_code}}/{{upload_for}}/`

* `lang_code` : i.e. en,ph etc
* `upload_for` : admin_panel or user_panel

* Result fields

Returns translated text as a key value pair

## Group Details
* To add group make a POST request to `/api/auth-group/` with following data parameters

* `name`: Str

* `description`: Str

* `permissions`: List


Results Fields

* `id`: Int

* `name`: Str

* `permissions`: List

After above API success response make post request to `/auth-api/driver-group/` pass value of the id of above API's 
response to group

* `group` : Int,

* `name`: Str,

* `description` : Str

Results Fields

* `id`: Int
  
* `name`: Str
  
* `group`: Int
  
* `description`: Str
  
* `is_admin`: Boolean

## Weather Info

To add weathe API providers info make a POST request to `/auth-api/weather-info/` with following data params


* `provider_name`: Str

* `client_id`: Int

* `client_secret`: Int

* `is_active`: Boolean


* To get weather API providers details make a GET request to `/auth-api/weather-info/`

Results Fields

* `id`: Int

* `provider_name`: Str

* `client_id`: Int

* `client_secret`: Int

* `is_active`: Boolean

* `created_at`: DateTime

* `is_deleted`: Boolean


* To delete weather API providers details make a DELETE request to `/auth-api/weather-info-details/{id}/`



* To add the choices for list of weathers make a POST request to with list of ids `/api/weather-data-list/`

`ids`: [2, 3,...]

To get list of values for weather make a GET request to `/api/weather-data-list/`

Results Fields

* `id`: Int

* `label`: Str

* `value`: Str

* `active`:  Boolean

## Crash Type

* To get the details of crash type make GET request to `/data-api/bindcrashtype/{uuid_of_recordtype}/`


To get the details of a groups make a GET request to `/api/auth-group/` it will return all of the groups with their 
permissions

* Results Fields


* `id`: Int

* `name`: Str

* `permissions` : List

## Bulk Upload

* To get detailed list of files added for bulk upload make a GET request to `/api/bulk-upload-details/`

* Result fields

[
  {
    id: Int,
    file_name: Str,
    file_status: Str,
    csv_uploaded_date: DateTime,
    record_type: Str
  },........
]

* To upload records in bulk make a POST request to `/api/bulkupload/` with the following data parameters


* `jsondata`: data:text/csv;base64,(Base 64 of a file that contains records in bulk)
* `upload_for`: Str(Incident, Intervention)
* `record_type`: UUID


* To get the details of duplicate record make GET request to `/api/duplicate-record-list/{{UUID}}/`
 
## Crash Factor Matrix

* For getting the details of crash factor matrix make GET request to `/api/getrecords/`

* Query params

* `archived` : Boolean

* `jsonb` : Object

* Query the data fields of the object and filter on the result.

    * Keys in this object mimic the search paths to filter on a particular object field. However, in place of values, a filter rule definition is used. Example:
`{ "accidentDetails": {
    "Main+cause": {
        "_rule_type": "containment",
        "contains": [
            "Vehicle+defect",
            "Road+defect",
            ["Vehicle+defect"],
            ["Road+defect"]
        ]
    },
    "Num+driver+casualties": {
        "_rule_type": "intrange",
        "min": 1,
        "max": 3
    }
}}` 
      
* `polygon`=UUID
      
* `limit`=Int

* `occurred_max`=DateTime

* `occurred_min`=DateTime

* `record_type`=UUID

* `tilekey`=Boolean

* Results fields

* `Crash number`: Int

* `Date`: day-month: 04-06

* `Date`: year: 2021

* `Day of week`: Str

* `Time of day`: 16:13

* `Severity`: List

* `light`: Str

* `DCA code`: Int
