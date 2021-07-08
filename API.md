#####DRIVER2.0

**URL**

http://{{ip}}:{{port}}/api/registration/

**METHOD**

  POST

**Data Params**

{
  "username": "david.turner",
  "password": "Admin@123",
  "first_name": "David",
  "last_name": "Turner",
  "email": "david.turner@gmail.com",
  "groups": [
    "Public"
  ],
  "is_staff": "False"
}

**Response**

[
  {
    "groupdetail": [
      "Public",
      1
    ],
    "token": "acdc96bea52782f7b362ccee1e4de9b8eb5365d2",
    "id": 4004,
    "first_name": "David",
    "last_name": "Turner",
    "username": "david.turner",
    "groups": [
      "Public"
    ],
    "email": "david.turner@gmail.com",
    "date_joined": "2021-07-05T12:36:09.700035+05:30",
    "is_staff": false,
    "is_superuser": false
  }
]

**URL**

http://{{ip}}:{{port}}/auth-api/adv-registration/

**METHOD**

  POST

**Data Params**

{
  "username": "david.turner",
  "password": "David@123",
  "first_name": "David",
  "last_name": "Turner",
  "email": "david.turner@gmail.com",
  "groups": [],
  "geography": "",
  "is_staff": "False",
  "user": 4004
}

**Response**

[
  {
    "id": 4004,
    "first_name": "David",
    "last_name": "Turner",
    "email": "david.turner@gmail.com",
    "username": "david.turner",
    "geography": "",
    "reg": [],
    "city": [],
    "org": [],
    "groups": [
      "Public"
    ],
    "is_active": true,
    "date_joined": "2021-07-05T12:36:10.175224+05:30",
    "updated_on": "2021-07-05T12:36:10.175244+05:30",
    "user": 4004,
    "is_role_requested": "Not Requested",
    "mobile_no": null,
    "is_staff": false,
    "is_superuser": false,
    "is_analyst": false,
    "is_tech_analyst": false,
    "google_user": false
  }
]


**URL**

http://{{ip}}:{{port}}/auth-api/api-token-auth/

**METHOD**

  POST

**Data Params**

{
    "username":"david.turner",
    "password":"Admin@123"
}

**Response**

[
  {
    "token": "acdc96bea52782f7b362ccee1e4de9b8eb5365d2",
    "username": "david.turner",
    "group": [
      "Public",
      1
    ],
    "user": 4004,
    "first name": "David",
    "last name": "Turner",
    "email_address": "david.turner@gmail.com",
    "active": true,
    "staff_status": false,
    "superuser_status": false,
    "is_analyst": false,
    "is_tech_analyst": false
  }
]

**URL**

/api/return-token/4004/

**METHOD**

  GET

**RESPONSE**

[
  {
    "data": {
      "groupdetail": [
        2,
        "Admin"
      ],
      "key": "f1aa00d42ee8c1eb690773afad9327c467ab9fab"
    },
    "message": "Success",
    "status": true
  }
]

**URL**

http://{{ip}}:{{port}}/auth-api/google-login/

**METHOD**

  POST

**Data Params**

{
	"email": "test@gmail.com",
	"name": "test",
	"groups": ["public"]
}

**URL**

/auth-api/user-info/2/

**METHOD**

  GET

**RESPONSE**

[
  {
    "data": [
      {
        "groupdetail": [
          2
        ],
        "token": "cxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx8",
        "id": 2,
        "first_name": "",
        "last_name": "",
        "username": "demo",
        "email": "test@gmail.com",
        "groups": [
          "admin"
        ],
        "is_staff": true,
        "is_superuser": true,
        "is_active": true,
        "date_joined": "2018-01-22T21:35:57Z"
      }
    ],
    "message": "success",
    "status": true
  }
]

**URL**

http://{{ip}}:{{port}}/api/country-info/

**Data Params**

{
    "country_code": "NZ",
    "country_name": "New Zealand",
    "latitude": 12.4394739437943,
    "longitude": 134.8948934839
}

**URL**

http://{{ip}}:{{port}}/api/language-details/

**METHOD**

  POST

**Data Params**

{
    "label": "En",
    "upload_for": "admin_panel",
    "language_code": "en",
    "csv_f": "application/vnd.ms-excel;base64",
    "default_for_user_panel": false,
    "default_for_admin_panel": true,
    "archive": false
}


**URL**

http://{{ip}}:{{port}}/auth-group/

**METHOD**

  POST

**Data Params**

{
    "name": "Admin",
    "description":"Group description",
    "permissions": [41,42,43,44]
}

**Response**

[
  {
    "data": {
      "id": 6,
      "name": "Admin",
      "permissions": [
        41,
        42,
        43,
        44
      ]
    },
    "message": "Data saved successfully",
    "status": true
  }
]

**URL**

/auth-api/driver-group/

**METHOD**

  POST

**Data Params**

{
  "group": 6,
  "name": "Admin",
  "description": "Group Description"
}

**Response**

[
  {
    "Data": {
      "id": 50,
      "name": "Admin",
      "group": 6,
      "description": "Group Description",
      "is_admin": false
    },
    "message": "Data saved successfully",
    "status": true
  }
]

**URL**

/auth-api/weather-info/

**METHOD**

  POST

**Data Params**

{
  "provider_name": "Openweather Map",
  "client_id": "8XXXXXXXXXXXXXXXXXXXXX1",
  "client_secret": "XXXX",
  "is_active": true
}

**RESPONSE**

{
  "message": "Details added successfully",
  "status": true
}

**URL**

/auth-api/weather-info/

**METHOD**

  GET

**RESPONSE**

{
  "data": [
    {
      "id": 1,
      "provider_name": "Openweather Map",
      "client_id": "8XXXXXXXXXXXXXXXXXXXXX1",
      "client_secret": "XXXX",
      "is_active": false,
      "created_at": "2021-07-05T11:35:54.517779Z",
      "is_deleted": false
    }
  ],
  "status": true
}

**URL**

/auth-api/weather-info-details/id/

**METHOD**

  DELETE

**RESPONSE**

[
  {
    "message": "Details deleted successfully",
    "status": true
  }
]



**URL**

/api/weather-data-list/

**METHOD**

  POST

**Data Params**

{
  "ids": [
    2,
    3,...
  ]
}

**URL**

/api/weather-data-list/

**METHOD**

  GET


**RESPONSE**

[
  {
    "id": 1,
    "label": "Clear day",
    "value": "clear-day",
    "active": true
  },..........
]

**URL**

/api/recordtypes/

**METHOD**

  GET

**RESPONSE**

[
  {
    "uuid": "1c04abed-f6ef-4ff0-87cd-734fbe4c767e",
    "current_schema": "64ab35fc-b9bc-4eac-8200-ab1734131d4a",
    "created": "2018-01-22T20:21:39.469095Z",
    "modified": "2018-02-05T05:44:52.046693Z",
    "label": "Incident",
    "plural_label": "Incidents",
    "description": "Incidents",
    "active": true,
    "geometry_type": "point",
    "temporal": true
  },
  {
    "uuid": "e83d8cc8-9bd5-406c-a471-a5e7e3b02386",
    "current_schema": "b379f86c-917d-465e-8a05-d324d5d2670f",
    "created": "2021-06-11T14:58:03.336278Z",
    "modified": "2021-06-11T14:58:03.336313Z",
    "label": "Intervention",
    "plural_label": "Interventions",
    "description": "Interventions",
    "active": true,
    "geometry_type": "point",
    "temporal": true
  }
]

**URL**

/data-api/bindcrashtype/uuid_of_recordtype/

**METHOD**

  GET

**URL**

/api/boundaries/

**METHOD**

  GET

**RESPONSE**

[
  {
    "uuid": "fa146d5b-600c-4273-ad68-119f5c1d06ab",
    "label": "City/Province",
    "color": "red",
    "display_field": "name",
    "data_fields": [
      "fips",
      "name",
      "note",
      "type",
      "admin",
      "gn_id",
      "gn_a3",
      "abbrev",
      "gns_id",
      "iso_a2",
      "postal",
      "region",
      "sov_a3",
      "woe_id",
      "adm0_a3",
      "adm0_sr",
      "diss_me",
      "gn_name",
      "type_en",
      "check_me",
      "datarank",
      "fips_alt",
      "geonunit",
      "gn_level",
      "gns_adm1",
      "gns_lang",
      "gns_name",
      "latitude",
      "name_alt",
      "name_len",
      "sub_code",
      "woe_name",
      "adm1_code",
      "area_sqkm",
      "code_hasc",
      "gn_region",
      "gns_level",
      "labelrank",
      "longitude",
      "mapcolor9",
      "scalerank",
      "wikipedia",
      "woe_label",
      "objectid_1",
      "adm0_label",
      "adm1_cod_1",
      "code_local",
      "featurecla",
      "gadm_level",
      "gn_a1_code",
      "gns_region",
      "hasc_maybe",
      "iso_3166_2",
      "mapcolor13",
      "name_local",
      "provnum_ne",
      "region_cod",
      "region_sub",
      "sameascity",
      "uuid"
    ],
    "errors": null,
    "created": "2021-07-05T08:24:14.901907Z",
    "modified": "2021-07-05T08:25:09.549569Z",
    "status": "COMPLETE",
    "source_file": "http://127.0.0.1:8000/api/boundaries/boundaries/2021/07/05/city_new.zip"
  },
  {
    "uuid": "45e1fb55-b1af-4d0f-b1a1-60d9f5a253d7",
    "label": "States",
    "color": "red",
    "display_field": "NAME_1",
    "data_fields": [
      "ID_0",
      "ISO",
      "NAME_0",
      "ID_1",
      "NAME_1",
      "TYPE_1",
      "ENGTYPE_1",
      "NL_NAME_1",
      "VARNAME_1"
    ],
    "errors": null,
    "created": "2018-01-22T20:27:31.668576Z",
    "modified": "2018-07-06T07:06:52.852305Z",
    "status": "COMPLETE",
    "source_file": "http://127.0.0.1:8000/api/boundaries/boundaries/2018/01/23/IND_adm.zip"
  }
]

**URL**

/api/auth-group/

**METHOD**

  GET

**RESPONSE**

[
  {
    "data": [
      {
        "id": 2,
        "name": "admin",
        "permissions": [
          {
            "id": 1,
            "name": "Can add log entry",
            "content_type": 1,
            "codename": "add_logentry"
          },
          {
            "id": 2,
            "name": "Can change log entry",
            "content_type": 1,
            "codename": "change_logentry"
          },
          {
            "id": 3,
            "name": "Can delete log entry",
            "content_type": 1,
            "codename": "delete_logentry"
          },
          {
            "id": 4,
            "name": "Can view log entry",
            "content_type": 1,
            "codename": "view_logentry"
          },
          {
            "id": 9,
            "name": "Can add group",
            "content_type": 3,
            "codename": "add_group"
          },
          {
            "id": 10,
            "name": "Can change group",
            "content_type": 3,
            "codename": "change_group"
          },
          {
            "id": 11,
            "name": "Can delete group",
            "content_type": 3,
            "codename": "delete_group"
          },
          {
            "id": 12,
            "name": "Can view group",
            "content_type": 3,
            "codename": "view_group"
          },
          {
            "id": 5,
            "name": "Can add permission",
            "content_type": 2,
            "codename": "add_permission"
          },
          {
            "id": 6,
            "name": "Can change permission",
            "content_type": 2,
            "codename": "change_permission"
          },
          {
            "id": 7,
            "name": "Can delete permission",
            "content_type": 2,
            "codename": "delete_permission"
          },
          {
            "id": 8,
            "name": "Can view permission",
            "content_type": 2,
            "codename": "view_permission"
          },
          {
            "id": 13,
            "name": "Can add user",
            "content_type": 4,
            "codename": "add_user"
          },
          {
            "id": 14,
            "name": "Can change user",
            "content_type": 4,
            "codename": "change_user"
          },
          {
            "id": 15,
            "name": "Can delete user",
            "content_type": 4,
            "codename": "delete_user"
          },
          {
            "id": 16,
            "name": "Can view user",
            "content_type": 4,
            "codename": "view_user"
          },
          {
            "id": 29,
            "name": "Can add Token",
            "content_type": 8,
            "codename": "add_token"
          },
          {
            "id": 30,
            "name": "Can change Token",
            "content_type": 8,
            "codename": "change_token"
          },
          {
            "id": 31,
            "name": "Can delete Token",
            "content_type": 8,
            "codename": "delete_token"
          },
          {
            "id": 32,
            "name": "Can view Token",
            "content_type": 8,
            "codename": "view_token"
          },
          {
            "id": 133,
            "name": "Can add black spot",
            "content_type": 34,
            "codename": "add_blackspot"
          },
          {
            "id": 134,
            "name": "Can change black spot",
            "content_type": 34,
            "codename": "change_blackspot"
          },
          {
            "id": 135,
            "name": "Can delete black spot",
            "content_type": 34,
            "codename": "delete_blackspot"
          },
          {
            "id": 136,
            "name": "Can view black spot",
            "content_type": 34,
            "codename": "view_blackspot"
          },
          {
            "id": 137,
            "name": "Can add black spot config",
            "content_type": 35,
            "codename": "add_blackspotconfig"
          },
          {
            "id": 138,
            "name": "Can change black spot config",
            "content_type": 35,
            "codename": "change_blackspotconfig"
          },
          {
            "id": 139,
            "name": "Can delete black spot config",
            "content_type": 35,
            "codename": "delete_blackspotconfig"
          },
          {
            "id": 140,
            "name": "Can view black spot config",
            "content_type": 35,
            "codename": "view_blackspotconfig"
          },
          {
            "id": 141,
            "name": "Can add black spot records file",
            "content_type": 36,
            "codename": "add_blackspotrecordsfile"
          },
          {
            "id": 142,
            "name": "Can change black spot records file",
            "content_type": 36,
            "codename": "change_blackspotrecordsfile"
          },
          {
            "id": 143,
            "name": "Can delete black spot records file",
            "content_type": 36,
            "codename": "delete_blackspotrecordsfile"
          },
          {
            "id": 144,
            "name": "Can view black spot records file",
            "content_type": 36,
            "codename": "view_blackspotrecordsfile"
          },
          {
            "id": 145,
            "name": "Can add black spot set",
            "content_type": 37,
            "codename": "add_blackspotset"
          },
          {
            "id": 146,
            "name": "Can change black spot set",
            "content_type": 37,
            "codename": "change_blackspotset"
          },
          {
            "id": 147,
            "name": "Can delete black spot set",
            "content_type": 37,
            "codename": "delete_blackspotset"
          },
          {
            "id": 148,
            "name": "Can view black spot set",
            "content_type": 37,
            "codename": "view_blackspotset"
          },
          {
            "id": 149,
            "name": "Can add black spot training csv",
            "content_type": 38,
            "codename": "add_blackspottrainingcsv"
          },
          {
            "id": 150,
            "name": "Can change black spot training csv",
            "content_type": 38,
            "codename": "change_blackspottrainingcsv"
          },
          {
            "id": 151,
            "name": "Can delete black spot training csv",
            "content_type": 38,
            "codename": "delete_blackspottrainingcsv"
          },
          {
            "id": 152,
            "name": "Can view black spot training csv",
            "content_type": 38,
            "codename": "view_blackspottrainingcsv"
          },
          {
            "id": 153,
            "name": "Can add load forecast training csv",
            "content_type": 39,
            "codename": "add_loadforecasttrainingcsv"
          },
          {
            "id": 154,
            "name": "Can change load forecast training csv",
            "content_type": 39,
            "codename": "change_loadforecasttrainingcsv"
          },
          {
            "id": 155,
            "name": "Can delete load forecast training csv",
            "content_type": 39,
            "codename": "delete_loadforecasttrainingcsv"
          },
          {
            "id": 156,
            "name": "Can view load forecast training csv",
            "content_type": 39,
            "codename": "view_loadforecasttrainingcsv"
          },
          {
            "id": 157,
            "name": "Can add road segments shapefile",
            "content_type": 40,
            "codename": "add_roadsegmentsshapefile"
          },
          {
            "id": 158,
            "name": "Can change road segments shapefile",
            "content_type": 40,
            "codename": "change_roadsegmentsshapefile"
          },
          {
            "id": 159,
            "name": "Can delete road segments shapefile",
            "content_type": 40,
            "codename": "delete_roadsegmentsshapefile"
          },
          {
            "id": 160,
            "name": "Can view road segments shapefile",
            "content_type": 40,
            "codename": "view_roadsegmentsshapefile"
          },
          {
            "id": 17,
            "name": "Can add content type",
            "content_type": 5,
            "codename": "add_contenttype"
          },
          {
            "id": 18,
            "name": "Can change content type",
            "content_type": 5,
            "codename": "change_contenttype"
          },
          {
            "id": 19,
            "name": "Can delete content type",
            "content_type": 5,
            "codename": "delete_contenttype"
          },
          {
            "id": 20,
            "name": "Can view content type",
            "content_type": 5,
            "codename": "view_contenttype"
          },
          {
            "id": 81,
            "name": "Can add bulk upload detail",
            "content_type": 21,
            "codename": "add_bulkuploaddetail"
          },
          {
            "id": 82,
            "name": "Can change bulk upload detail",
            "content_type": 21,
            "codename": "change_bulkuploaddetail"
          },
          {
            "id": 83,
            "name": "Can delete bulk upload detail",
            "content_type": 21,
            "codename": "delete_bulkuploaddetail"
          },
          {
            "id": 84,
            "name": "Can view bulk upload detail",
            "content_type": 21,
            "codename": "view_bulkuploaddetail"
          },
          {
            "id": 85,
            "name": "Can add crash diagram orientation",
            "content_type": 22,
            "codename": "add_crashdiagramorientation"
          },
          {
            "id": 86,
            "name": "Can change crash diagram orientation",
            "content_type": 22,
            "codename": "change_crashdiagramorientation"
          },
          {
            "id": 87,
            "name": "Can delete crash diagram orientation",
            "content_type": 22,
            "codename": "delete_crashdiagramorientation"
          },
          {
            "id": 88,
            "name": "Can view crash diagram orientation",
            "content_type": 22,
            "codename": "view_crashdiagramorientation"
          },
          {
            "id": 89,
            "name": "Can add dedupe job",
            "content_type": 23,
            "codename": "add_dedupejob"
          },
          {
            "id": 90,
            "name": "Can change dedupe job",
            "content_type": 23,
            "codename": "change_dedupejob"
          },
          {
            "id": 91,
            "name": "Can delete dedupe job",
            "content_type": 23,
            "codename": "delete_dedupejob"
          },
          {
            "id": 92,
            "name": "Can view dedupe job",
            "content_type": 23,
            "codename": "view_dedupejob"
          },
          {
            "id": 93,
            "name": "Can add driver record",
            "content_type": 24,
            "codename": "add_driverrecord"
          },
          {
            "id": 94,
            "name": "Can change driver record",
            "content_type": 24,
            "codename": "change_driverrecord"
          },
          {
            "id": 95,
            "name": "Can delete driver record",
            "content_type": 24,
            "codename": "delete_driverrecord"
          },
          {
            "id": 96,
            "name": "Can view driver record",
            "content_type": 24,
            "codename": "view_driverrecord"
          },
          {
            "id": 97,
            "name": "Can add driver record copy",
            "content_type": 25,
            "codename": "add_driverrecordcopy"
          },
          {
            "id": 98,
            "name": "Can change driver record copy",
            "content_type": 25,
            "codename": "change_driverrecordcopy"
          },
          {
            "id": 99,
            "name": "Can delete driver record copy",
            "content_type": 25,
            "codename": "delete_driverrecordcopy"
          },
          {
            "id": 100,
            "name": "Can view driver record copy",
            "content_type": 25,
            "codename": "view_driverrecordcopy"
          },
          {
            "id": 101,
            "name": "Can add duplicate distance config",
            "content_type": 26,
            "codename": "add_duplicatedistanceconfig"
          },
          {
            "id": 102,
            "name": "Can change duplicate distance config",
            "content_type": 26,
            "codename": "change_duplicatedistanceconfig"
          },
          {
            "id": 103,
            "name": "Can delete duplicate distance config",
            "content_type": 26,
            "codename": "delete_duplicatedistanceconfig"
          },
          {
            "id": 104,
            "name": "Can view duplicate distance config",
            "content_type": 26,
            "codename": "view_duplicatedistanceconfig"
          },
          {
            "id": 105,
            "name": "Can add irap detail",
            "content_type": 27,
            "codename": "add_irapdetail"
          },
          {
            "id": 106,
            "name": "Can change irap detail",
            "content_type": 27,
            "codename": "change_irapdetail"
          },
          {
            "id": 107,
            "name": "Can delete irap detail",
            "content_type": 27,
            "codename": "delete_irapdetail"
          },
          {
            "id": 108,
            "name": "Can view irap detail",
            "content_type": 27,
            "codename": "view_irapdetail"
          },
          {
            "id": 129,
            "name": "Can add key detail",
            "content_type": 33,
            "codename": "add_keydetail"
          },
          {
            "id": 130,
            "name": "Can change key detail",
            "content_type": 33,
            "codename": "change_keydetail"
          },
          {
            "id": 131,
            "name": "Can delete key detail",
            "content_type": 33,
            "codename": "delete_keydetail"
          },
          {
            "id": 132,
            "name": "Can view key detail",
            "content_type": 33,
            "codename": "view_keydetail"
          },
          {
            "id": 109,
            "name": "Can add record audit log entry",
            "content_type": 28,
            "codename": "add_recordauditlogentry"
          },
          {
            "id": 110,
            "name": "Can change record audit log entry",
            "content_type": 28,
            "codename": "change_recordauditlogentry"
          },
          {
            "id": 111,
            "name": "Can delete record audit log entry",
            "content_type": 28,
            "codename": "delete_recordauditlogentry"
          },
          {
            "id": 112,
            "name": "Can view record audit log entry",
            "content_type": 28,
            "codename": "view_recordauditlogentry"
          },
          {
            "id": 113,
            "name": "Can add record cost config",
            "content_type": 29,
            "codename": "add_recordcostconfig"
          },
          {
            "id": 114,
            "name": "Can change record cost config",
            "content_type": 29,
            "codename": "change_recordcostconfig"
          },
          {
            "id": 115,
            "name": "Can delete record cost config",
            "content_type": 29,
            "codename": "delete_recordcostconfig"
          },
          {
            "id": 116,
            "name": "Can view record cost config",
            "content_type": 29,
            "codename": "view_recordcostconfig"
          },
          {
            "id": 117,
            "name": "Can add record duplicate",
            "content_type": 30,
            "codename": "add_recordduplicate"
          },
          {
            "id": 118,
            "name": "Can change record duplicate",
            "content_type": 30,
            "codename": "change_recordduplicate"
          },
          {
            "id": 119,
            "name": "Can delete record duplicate",
            "content_type": 30,
            "codename": "delete_recordduplicate"
          },
          {
            "id": 120,
            "name": "Can view record duplicate",
            "content_type": 30,
            "codename": "view_recordduplicate"
          },
          {
            "id": 121,
            "name": "Can add weather data list",
            "content_type": 31,
            "codename": "add_weatherdatalist"
          },
          {
            "id": 122,
            "name": "Can change weather data list",
            "content_type": 31,
            "codename": "change_weatherdatalist"
          },
          {
            "id": 123,
            "name": "Can delete weather data list",
            "content_type": 31,
            "codename": "delete_weatherdatalist"
          },
          {
            "id": 124,
            "name": "Can view weather data list",
            "content_type": 31,
            "codename": "view_weatherdatalist"
          },
          {
            "id": 125,
            "name": "Can add weather info",
            "content_type": 32,
            "codename": "add_weatherinfo"
          },
          {
            "id": 126,
            "name": "Can change weather info",
            "content_type": 32,
            "codename": "change_weatherinfo"
          },
          {
            "id": 127,
            "name": "Can delete weather info",
            "content_type": 32,
            "codename": "delete_weatherinfo"
          },
          {
            "id": 128,
            "name": "Can view weather info",
            "content_type": 32,
            "codename": "view_weatherinfo"
          },
          {
            "id": 53,
            "name": "Can add city",
            "content_type": 14,
            "codename": "add_city"
          },
          {
            "id": 54,
            "name": "Can change city",
            "content_type": 14,
            "codename": "change_city"
          },
          {
            "id": 55,
            "name": "Can delete city",
            "content_type": 14,
            "codename": "delete_city"
          },
          {
            "id": 56,
            "name": "Can view city",
            "content_type": 14,
            "codename": "view_city"
          },
          {
            "id": 57,
            "name": "Can add country info",
            "content_type": 15,
            "codename": "add_countryinfo"
          },
          {
            "id": 58,
            "name": "Can change country info",
            "content_type": 15,
            "codename": "change_countryinfo"
          },
          {
            "id": 59,
            "name": "Can delete country info",
            "content_type": 15,
            "codename": "delete_countryinfo"
          },
          {
            "id": 60,
            "name": "Can view country info",
            "content_type": 15,
            "codename": "view_countryinfo"
          },
          {
            "id": 61,
            "name": "Can add groupdetail",
            "content_type": 16,
            "codename": "add_groupdetail"
          },
          {
            "id": 62,
            "name": "Can change groupdetail",
            "content_type": 16,
            "codename": "change_groupdetail"
          },
          {
            "id": 63,
            "name": "Can delete groupdetail",
            "content_type": 16,
            "codename": "delete_groupdetail"
          },
          {
            "id": 64,
            "name": "Can view groupdetail",
            "content_type": 16,
            "codename": "view_groupdetail"
          },
          {
            "id": 65,
            "name": "Can add language detail",
            "content_type": 17,
            "codename": "add_languagedetail"
          },
          {
            "id": 66,
            "name": "Can change language detail",
            "content_type": 17,
            "codename": "change_languagedetail"
          },
          {
            "id": 67,
            "name": "Can delete language detail",
            "content_type": 17,
            "codename": "delete_languagedetail"
          },
          {
            "id": 68,
            "name": "Can view language detail",
            "content_type": 17,
            "codename": "view_languagedetail"
          },
          {
            "id": 69,
            "name": "Can add organization",
            "content_type": 18,
            "codename": "add_organization"
          },
          {
            "id": 70,
            "name": "Can change organization",
            "content_type": 18,
            "codename": "change_organization"
          },
          {
            "id": 71,
            "name": "Can delete organization",
            "content_type": 18,
            "codename": "delete_organization"
          },
          {
            "id": 72,
            "name": "Can view organization",
            "content_type": 18,
            "codename": "view_organization"
          },
          {
            "id": 77,
            "name": "Can add user detail",
            "content_type": 20,
            "codename": "add_userdetail"
          },
          {
            "id": 78,
            "name": "Can change user detail",
            "content_type": 20,
            "codename": "change_userdetail"
          },
          {
            "id": 79,
            "name": "Can delete user detail",
            "content_type": 20,
            "codename": "delete_userdetail"
          },
          {
            "id": 80,
            "name": "Can view user detail",
            "content_type": 20,
            "codename": "view_userdetail"
          },
          {
            "id": 33,
            "name": "Can add Boundary",
            "content_type": 9,
            "codename": "add_boundary"
          },
          {
            "id": 34,
            "name": "Can change Boundary",
            "content_type": 9,
            "codename": "change_boundary"
          },
          {
            "id": 35,
            "name": "Can delete Boundary",
            "content_type": 9,
            "codename": "delete_boundary"
          },
          {
            "id": 36,
            "name": "Can view Boundary",
            "content_type": 9,
            "codename": "view_boundary"
          },
          {
            "id": 37,
            "name": "Can add Boundary Polygon",
            "content_type": 10,
            "codename": "add_boundarypolygon"
          },
          {
            "id": 38,
            "name": "Can change Boundary Polygon",
            "content_type": 10,
            "codename": "change_boundarypolygon"
          },
          {
            "id": 39,
            "name": "Can delete Boundary Polygon",
            "content_type": 10,
            "codename": "delete_boundarypolygon"
          },
          {
            "id": 40,
            "name": "Can view Boundary Polygon",
            "content_type": 10,
            "codename": "view_boundarypolygon"
          },
          {
            "id": 41,
            "name": "Can add record",
            "content_type": 11,
            "codename": "add_record"
          },
          {
            "id": 42,
            "name": "Can change record",
            "content_type": 11,
            "codename": "change_record"
          },
          {
            "id": 43,
            "name": "Can delete record",
            "content_type": 11,
            "codename": "delete_record"
          },
          {
            "id": 44,
            "name": "Can view record",
            "content_type": 11,
            "codename": "view_record"
          },
          {
            "id": 45,
            "name": "Can add record schema",
            "content_type": 12,
            "codename": "add_recordschema"
          },
          {
            "id": 46,
            "name": "Can change record schema",
            "content_type": 12,
            "codename": "change_recordschema"
          },
          {
            "id": 47,
            "name": "Can delete record schema",
            "content_type": 12,
            "codename": "delete_recordschema"
          },
          {
            "id": 48,
            "name": "Can view record schema",
            "content_type": 12,
            "codename": "view_recordschema"
          },
          {
            "id": 49,
            "name": "Can add record type",
            "content_type": 13,
            "codename": "add_recordtype"
          },
          {
            "id": 50,
            "name": "Can change record type",
            "content_type": 13,
            "codename": "change_recordtype"
          },
          {
            "id": 51,
            "name": "Can delete record type",
            "content_type": 13,
            "codename": "delete_recordtype"
          },
          {
            "id": 52,
            "name": "Can view record type",
            "content_type": 13,
            "codename": "view_recordtype"
          },
          {
            "id": 21,
            "name": "Can add session",
            "content_type": 6,
            "codename": "add_session"
          },
          {
            "id": 22,
            "name": "Can change session",
            "content_type": 6,
            "codename": "change_session"
          },
          {
            "id": 23,
            "name": "Can delete session",
            "content_type": 6,
            "codename": "delete_session"
          },
          {
            "id": 24,
            "name": "Can view session",
            "content_type": 6,
            "codename": "view_session"
          },
          {
            "id": 25,
            "name": "Can add site",
            "content_type": 7,
            "codename": "add_site"
          },
          {
            "id": 26,
            "name": "Can change site",
            "content_type": 7,
            "codename": "change_site"
          },
          {
            "id": 27,
            "name": "Can delete site",
            "content_type": 7,
            "codename": "delete_site"
          },
          {
            "id": 28,
            "name": "Can view site",
            "content_type": 7,
            "codename": "view_site"
          },
          {
            "id": 161,
            "name": "Can add saved filter",
            "content_type": 41,
            "codename": "add_savedfilter"
          },
          {
            "id": 162,
            "name": "Can change saved filter",
            "content_type": 41,
            "codename": "change_savedfilter"
          },
          {
            "id": 163,
            "name": "Can delete saved filter",
            "content_type": 41,
            "codename": "delete_savedfilter"
          },
          {
            "id": 164,
            "name": "Can view saved filter",
            "content_type": 41,
            "codename": "view_savedfilter"
          }
        ]
      },
      {
        "id": 3,
        "name": "analyst",
        "permissions": []
      },
      {
        "id": 6,
        "name": "Group1",
        "permissions": [
          {
            "id": 1,
            "name": "Can add log entry",
            "content_type": 1,
            "codename": "add_logentry"
          },
          {
            "id": 2,
            "name": "Can change log entry",
            "content_type": 1,
            "codename": "change_logentry"
          },
          {
            "id": 3,
            "name": "Can delete log entry",
            "content_type": 1,
            "codename": "delete_logentry"
          },
          {
            "id": 4,
            "name": "Can view log entry",
            "content_type": 1,
            "codename": "view_logentry"
          },
          {
            "id": 5,
            "name": "Can add permission",
            "content_type": 2,
            "codename": "add_permission"
          },
          {
            "id": 6,
            "name": "Can change permission",
            "content_type": 2,
            "codename": "change_permission"
          },
          {
            "id": 7,
            "name": "Can delete permission",
            "content_type": 2,
            "codename": "delete_permission"
          },
          {
            "id": 8,
            "name": "Can view permission",
            "content_type": 2,
            "codename": "view_permission"
          }
        ]
      },
      {
        "id": 1,
        "name": "Public",
        "permissions": [
          {
            "id": 73,
            "name": "Can add send role request",
            "content_type": 19,
            "codename": "add_sendrolerequest"
          },
          {
            "id": 74,
            "name": "Can change send role request",
            "content_type": 19,
            "codename": "change_sendrolerequest"
          },
          {
            "id": 75,
            "name": "Can delete send role request",
            "content_type": 19,
            "codename": "delete_sendrolerequest"
          },
          {
            "id": 76,
            "name": "Can view send role request",
            "content_type": 19,
            "codename": "view_sendrolerequest"
          },
          {
            "id": 164,
            "name": "Can view saved filter",
            "content_type": 41,
            "codename": "view_savedfilter"
          }
        ]
      }
    ],
    "status": "true"
  }
]

**URL**

/api/country-info/?archived=true

**METHOD**

  GET

**RESPONSE**

[
  {
    "id": 2,
    "country_code": "in",
    "country_name": "India",
    "archived": true,
    "latitude": 19.80805412808859,
    "longitude": 73.21289062500001
  }
]

**URL**

/api/dedupe-config/

**METHOD**

  GET

**RESPONSE**

[
  {
    "id": 1,
    "dedupe_distance_threshold": 0.0009,
    "unit": "degree",
    "created": "2020-07-30T08:11:42.706240Z",
    "modified": "2020-07-30T08:11:42.706240Z"
  }
]

**URL**

/api/dedupe-config/id/

**METHOD**

  PATCH

**RESPONSE**

[
  {
    "id": 1,
    "dedupe_distance_threshold": 0.0009,
    "unit": "degree",
    "created": "2020-07-30T08:11:42.706240Z",
    "modified": "2020-07-30T08:11:42.706240Z"
  }
]

**URL**

/api/bulk-upload-details/

**METHOD**

  GET
  
**RESPONSE**

[
  {
    "id": 5,
    "file_name": "1623850491.csv",
    "file_status": "COMPLETED",
    "csv_uploaded_date": "2021-06-16T13:34:51.655485Z",
    "record_type": "Incident"
  }
]

**URL**

/api/bulkupload/

**METHOD**

  POST

**DATA PARAMS**

{
  "jsondata": "data:text/csv;base64,base_64goes_here",
  "upload_for": "incident",
  "record_type": "1c04abed-f6ef-4ff0-87cd-734fbe4c767e"
}

**RESPONSE**

{
  "data": {},
  "message": "All Data is Correct",
  "status": true
}

**URL**

/api/blackspotconfig/?limit=all

**METHOD**

  GET

**RESPONSE**

[
  {
    "uuid": "43eb74b8-26bd-4561-8ed7-fb5be5a8352b",
    "created": "2016-05-24T19:19:56.339703Z",
    "modified": "2018-01-23T02:38:07.272030Z",
    "severity_percentile_threshold": 0.95
  }
]

**URL**

/api/blackspotconfig/uuid/

**METHOD**

  PATCH

**DATA PARAMS**

{
  "severity_percentile_threshold": 0.95
}

**RESPONSE**

{
  "uuid": "43eb74b8-26bd-4561-8ed7-fb5be5a8352b",
  "created": "2016-05-24T19:19:56.339703Z",
  "modified": "2021-07-08T07:01:47.754287Z",
  "severity_percentile_threshold": 0.95
}

**URL**

/api/recordtypes/

**METHOD**

  POST

**REPSONSE**

{
  "uuid": "83884189-dc84-46d3-ac64-6932d3638483",
  "current_schema": null,
  "created": "2021-07-08T09:19:53.888783Z",
  "modified": "2021-07-08T09:19:53.888832Z",
  "label": "Incident1",
  "plural_label": "Incident1",
  "description": "Incidents",
  "active": true,
  "geometry_type": "point",
  "temporal": true
}
**URL**

/api/recordtypes/83884189-dc84-46d3-ac64-6932d3638483/

**METHOD**

  DELETE

**URL**

/data-api/latestrecordschema/

**METHOD**

  POST

**RESPONSE**

{
  "result": [
    {
      "uuid": "b379f86c-917d-465e-8a05-d324d5d2670f",
      "created": "2021-06-11T14:58:03.534143Z",
      "modified": "2021-06-11T14:58:03.534179Z",
      "version": 1,
      "schema": {
        "type": "object",
        "title": "",
        "$schema": "http://json-schema.org/draft-04/schema#",
        "properties": {
          "driverInterventionDetails": {
            "$ref": "#/definitions/driverInterventionDetails",
            "options": {
              "collapsed": true
            },
            "propertyOrder": 0
          }
        },
        "definitions": {
          "driverInterventionDetails": {
            "type": "object",
            "title": "Intervention Details",
            "details": true,
            "multiple": false,
            "properties": {},
            "definitions": {},
            "description": "Details for Intervention",
            "plural_title": "Intervention Details"
          }
        },
        "description": "",
        "record_type": "e83d8cc8-9bd5-406c-a471-a5e7e3b02386",
        "plural_title": ""
      },
      "next_version_id": null,
      "record_type_id": "e83d8cc8-9bd5-406c-a471-a5e7e3b02386"
    }
  ]
}

**URL**

/api/recordschemas/f825db2c-d182-4edc-8778-1b19452ed3b7/

**METHOD**

  GET

**URL**

/api/language-details/?archive=False

**METHOD**

  GET

**RESPONSE**

[
  {
    "id": 2,
    "label": "English",
    "csv_file": "https://mumbai.drivertool.org/download/multi-language/ashlar-editor/language-csv/en.csv",
    "json_file": "/var/www/static/media/multi-language/ashlar-editor/language-json/en.json",
    "language_code": "en",
    "upload_for": "admin_panel",
    "default_for_user_panel": false,
    "default_for_admin_panel": true,
    "archive": false,
    "created_date": "2021-05-01T09:36:08.107228Z",
    "updated_date": "2021-06-11T14:51:14.823704Z"
  }......
]

**URL**

/api/language-details/2/

**METHOD**

  GET

**RESPONSE**

{
  "id": 2,
  "label": "English",
  "csv_file": "https://mumbai.drivertool.org/download/multi-language/ashlar-editor/language-csv/en.csv",
  "json_file": "/var/www/static/media/multi-language/ashlar-editor/language-json/en.json",
  "language_code": "en",
  "upload_for": "admin_panel",
  "default_for_user_panel": false,
  "default_for_admin_panel": true,
  "archive": false,
  "created_date": "2021-05-01T09:36:08.107228Z",
  "updated_date": "2021-06-11T14:51:14.823704Z"
}

**URL**

/api/language-details/2/

**METHOD**

  PUT

**DATA PARAMETERS**

{
  "id": "2",
  "upload_for": "admin_panel",
  "language_code": "en",
  "label": "English",
  "csv_f": "data:text/csv;base64,",
  "default_for_user_panel": false,
  "default_for_admin_panel": true
}
  
**RESPONSE**

{
  "id": 2,
  "label": "English",
  "csv_file": "http://127.0.0.1:8000/download/multi-language/ashlar-editor/language-csv/en.csv",
  "json_file": "/var/www/static/media/multi-language/ashlar-editor/language-json/en.json",
  "language_code": "en",
  "upload_for": "admin_panel",
  "default_for_user_panel": false,
  "default_for_admin_panel": true,
  "archive": false,
  "created_date": "2021-05-01T09:36:08.107228Z",
  "updated_date": "2021-07-08T09:32:11.979884Z"
}

**URL**

/api/lang-json/en/admin_panel/
/api/lang-json/en/user_panel/

**METHOD**

  GET

**URL**

/api/userfilters/

**METHOD**

  GET

**URL**

/api/boundarypolygons/?active=True&boundary=fa146d5b-600c-4273-ad68-119f5c1d06ab&limit=all&nogeom=true

**METHOD**

  GET

**URL**

api/records/toddow/?search=&archived=False&details_only=True&occurred_max=2021-07-08T09:36:23.462Z&occurred_min=2021-04-09T09:36:23.462Z&polygon_id=&record_type=1c04abed-f6ef-4ff0-87cd-734fbe4c767e&jsonb=&polygon=

**METHOD**

  GET

**RESPONSE**

[
  {
    "dow": 6,
    "tod": 10,
    "count": 1
  },
  {
    "dow": 6,
    "tod": 16,
    "count": 1
  },
  {
    "dow": 1,
    "tod": 20,
    "count": 2
  },
  {
    "dow": 2,
    "tod": 20,
    "count": 1
  },
  {
    "dow": 6,
    "tod": 20,
    "count": 1
  },
  {
    "dow": 7,
    "tod": 20,
    "count": 1
  }
]

**URL**

/api/records/costs/?archived=False&occurred_min=2021-04-08T18:30:00.000Z&occurred_max=2021-07-08T09:36:23.464Z&polygon_id=&record_type=1c04abed-f6ef-4ff0-87cd-734fbe4c767e

**METHOD**

  GET

**RESPONSE**

{"prefix":"₹","suffix":"","total":"40,425,000","subtotals":{"Fatal":34650000,"Serious Injury":5775000,"Minor Injury":0,"Non Injury":0},"outdated_cost_config":false}


**URL**

/api/records/recent_counts/?archived=False&details_only=True&polygon_id=&record_type=1c04abed-f6ef-4ff0-87cd-734fbe4c767e

**METHOD**

  GET
  
**RESPONSE**

{"month":7,"quarter":7,"year":929}

**URL**

/api/blackspotsets/?effective_at=2021-07-08T09:36:23.469Z&limit=all&record_type=1c04abed-f6ef-4ff0-87cd-734fbe4c767e

**METHOD**

  GET
  
**RESPONSE**

[
  {
    "uuid": "190bafe1-d4f7-48a2-b06c-cfe64edd3ec3",
    "created": "2021-05-19T19:25:18.028812Z",
    "modified": "2021-05-19T19:25:18.028849Z",
    "effective_start": "2021-05-19T19:25:18.026185Z",
    "effective_end": null,
    "record_type": "1c04abed-f6ef-4ff0-87cd-734fbe4c767e"
  }
]

**URL**

/api/records/?archived=False&tilekey=true&polygon_id=&record_type=1c04abed-f6ef-4ff0-87cd-734fbe4c767e&occurred_min=2021-06-24T09:36:23.472Z

**METHOD**

  GET
  
**RESPONSE**

{"tilekey":"0f4dc125-f581-430a-ab85-4c9e964858ea"}

**URL**

/api/records/?details_only=True&search=&archived=False&limit=50&polygon_id=&polygon=&jsonb={%22driverIncidentDetails%22:{%22Severity%22:{%22_rule_type%22:%22containment%22,%22contains%22:[]}}}&polygon=&occurred_max=2021-07-08T09:58:44.071Z&occurred_min=2021-04-08T18:30:00.000Z&record_type=fe31e012-0d9b-4694-a86d-8c737e0c7672&tilekey=false

**METHOD**

  GET
  
**RESPONSE**

{
  "count": 739,
  "results": [
    {
      "uuid": "1b043f48-a08f-44ca-a600-c21c269fbfcc",
      "data": {
        "driverIncidentDetails": {
          "Severity": [
            "Property Damage"
          ],
          "_localId": "7cf621e1-51fd-42f8-ae69-8a3c898765c7",
          "Main cause": "Human error",
          "Description": "",
          "Collision type": "Side swipe",
          "Email of Encoder": "",
          "Reporting Agency": "MMDA Metrobase",
          "Location Approximate": []
        }
      },
      "created_by": "metrobase8@gmail.com",
      "created": "2021-07-08T03:53:06.255450Z",
      "modified": "2021-07-08T03:53:06.255494Z",
      "archived": false,
      "occurred_from": "2021-07-08T01:35:13Z",
      "occurred_to": "2021-07-08T03:50:13Z",
      "geom": {
        "type": "Point",
        "coordinates": [
          121.057036720306,
          14.5857353
        ]
      },
      "location_text": "SM Megamall Building A, SM Megamall, Wack-Wack Greenhills, Mandaluyong, 2nd District, NCR;MM, 1554, Luzon",
      "weather": "scattered clouds",
      "light": "",
      "city": null,
      "city_district": null,
      "county": null,
      "neighborhood": null,
      "road": null,
      "state": null,
      "merged_and_updated": false,
      "merged_uuid": null,
      "uploaded_from": "Web",
      "schema": "f825db2c-d182-4edc-8778-1b19452ed3b7"
    },....
}

**URL**

/api/records/1b043f48-a08f-44ca-a600-c21c269fbfcc/

**METHOD**

  GET
  
**RESPONSE**

{
  "uuid": "1b043f48-a08f-44ca-a600-c21c269fbfcc",
  "data": {
    "driverNotes": {
      "Notes": "",
      "_localId": "08ad1959-50df-4683-9467-cb5bf07b130e"
    },
    "driverPhoto": [],
    "driverPerson": [],
    "driverVehicle": [
      {
        "Make": "",
        "Model": "",
        "_localId": "674a612e-962c-49b8-84cd-d008991539ed",
        "Plate number": "DAE 3909",
        "Vehicle type": "Car",
        "Engine number": "",
        "Chassis number": "",
        "Classification": "Private",
        "Insurance details": ""
      },
      {
        "Make": "",
        "Model": "",
        "_localId": "6af552c3-a6bf-4584-a449-43cbef692b56",
        "Plate number": "DAN 1882",
        "Vehicle type": "SUV",
        "Engine number": "",
        "Chassis number": "",
        "Classification": "Private",
        "Insurance details": ""
      }
    ],
    "driverCrashDiagram": {
      "Image": "",
      "_localId": "b72a2bfa-e75e-4e7e-aa0f-31d75ca7e952",
      "Movement Code": ""
    },
    "driverIncidentDetails": {
      "Severity": [
        "Property Damage"
      ],
      "_localId": "7cf621e1-51fd-42f8-ae69-8a3c898765c7",
      "Main cause": "Human error",
      "Description": "",
      "Collision type": "Side swipe",
      "Email of Encoder": "",
      "Reporting Agency": "MMDA Metrobase",
      "Location Approximate": []
    }
  },
  "modified_by": "metrobase8@gmail.com",
  "created": "2021-07-08T03:53:06.255450Z",
  "modified": "2021-07-08T03:53:06.255494Z",
  "archived": false,
  "occurred_from": "2021-07-08T01:35:13Z",
  "occurred_to": "2021-07-08T03:50:13Z",
  "geom": {
    "type": "Point",
    "coordinates": [
      121.057036720306,
      14.5857353
    ]
  },
  "location_text": "SM Megamall Building A, SM Megamall, Wack-Wack Greenhills, Mandaluyong, 2nd District, NCR;MM, 1554, Luzon",
  "weather": "scattered clouds",
  "light": "",
  "city": null,
  "city_district": null,
  "county": null,
  "neighborhood": null,
  "road": null,
  "state": null,
  "merged_and_updated": false,
  "merged_uuid": null,
  "uploaded_from": "Web",
  "schema": "f825db2c-d182-4edc-8778-1b19452ed3b7"
}

**URL**

/api/record-copy-details/1b043f48-a08f-44ca-a600-c21c269fbfcc/

**METHOD**

  GET

