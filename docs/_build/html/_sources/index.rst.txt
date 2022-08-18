.. Cropin Plotrisk-Insight SDK documentation master file, created by
   sphinx-quickstart on Tue Jul 19 10:13:03 2022.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to Cropin Plotrisk-Insight SDK's documentation!
=======================================================

.. include:: install.rst

Cropin Plotrisk-Insight Client has functions to fetch plots, satellite, weather and yield details.
It also exposes the plot image download function.

Important Definitions
---------------------

**Plot** - A piece of land, represented by geojson structure i.e. Polygon, Multipolygon or a circle.

**Satellite Data** - For the plot created, satellite insights will be generated.

**Yield** - Yield mapping refers to the process of collecting georeferenced data on crop yield and characteristics, such as moisture content, while the crop is being harvested with an onboard yield monitor.

**Weather** - Weather data provides information about the weather and climate of a plot.

**GDD** - GDD (Cumulative growing degree days) is an index calculated from temperature data and is used to estimate the time needed for a crop or other organisms to reach a certain stage of development.

Prerequisites
-------------

1. **Supported Python Version** - This SDK has been tested with Python versions 3.5+.
Earlier Python 3 versions are expected to work as well, as long as the dependencies are fulfilled.

2. Users who have already onboarded onto sf_plus, enabled plotrisk feature for atleast few plots will be able use this SDK.


QUICKSTART
----------

.. code-block:: python


  from python_sdk_client.cropin_api import CropinAPI
  import json
  import logging
  import urllib

  """Example on how to use CropAPI.
  """
   if __name__ == '__main__':
       logging.info(">>>>>>>>>>>> starting")

       # authenticate
       cropin_api = CropinAPI("test", "12345678", "admin",env= EnvType.QA)

       # plot details without any filter
       plot_response = cropin_api.get_plot_details()
       print("plot details without any filters is : {}".format(plot_response))

       # satellite data without any filter
       satellite_response = cropin_api.get_satellite_details()
       print("satellite metrics with no filters :{}".format(satellite_response))

       # satellite data with boundary_id filter
       satellite_response = cropin_api.get_satellite_details(ca_ids='6801')
       print("satellite metrics when boundaryId is passed : {}".format(satellite_response))

       # # yield data without any filter
       yield_response = cropin_api.get_yield_details()
       print("yield data with no filter passed :{}".format(yield_response))
       #
       # # weather data without any filter
       weather_response = cropin_api.get_weather_details()
       print("weather data with no filter passed :{}".format(weather_response))
       #
       # # plot image download
       download_response = cropin_api.download_image(ca_id='6801', image_name='NDVI',
                                                     image_type='PNG', date='2022-06-30')
       print("download_response is: {}".format(download_response))

       # code to convert the bytes to image
       imgdata = base64.b64decode(download_response['bytes'])
       filename = 'image.jpg'
       with open(filename, 'wb') as f:
           f.write(imgdata)

Authentication
----------------

.. code-block:: python

  from python_sdk_client.cropin_api import CropinAPI

  cropin_api = CropinAPI("XXXX", "xyz", "xyz")

   #Exception when calling AuthenticateApi->get_token: (404)
   {
    "timestamp": "2022-07-06T04:21:52.563Z",
    "status": 404,
    "error": "XXXX" : tenant not found",
    "errorCode": "404 NOT_FOUND"
   }

   {
  "timestamp": "2022-07-11T13:02:27.241Z",
  "status": 401,
  "error": "Invalid input data",
  "errorCode": "UnauthorizedException"
   }
Either way, if you get an error 401 Unauthorized, your credentials were wrong or not yet active for the CropinApi you are contacting.

Get Plot Details
----------------

Parameters which can be passed as **kwargs or Optional Parameters
-----------------------------------------------------------------
        **MAX return size of response list is 5000**
.. code-block:: python

   import json
   import logging
   import urllib

   from python_sdk_client.cropin_api import CropinAPI

   plot_response = cropin_api.get_plot_details()
   print("plot details without any filters is : {}".format(plot_response))

   #respnse
      [
       {
           "id": 2602,
           "farmerCropId": 2,
           "name": "asset1/CA-1",
           "createdDate": "2021-09-24T11:48:06.356Z",
           "lastModifiedDate": "2022-08-10T11:20:16.729Z",
           "declaredArea": {
               "count": 1000.0
           },
           "auditedArea": null,
           "cropDetails": {
               "cropId": 2251,
               "cropName": "potatosub",
               "sowingDate": "2021-09-25T00:00:00Z",
               "expectedHarvestDate": "2024-06-21T00:00:00Z"
           }
       },
       {
           "id": 2601,
           "farmerCropId": 1,
           "name": "asset2/CA-1",
           "createdDate": "2021-09-24T11:48:06.235Z",
           "lastModifiedDate": "2022-04-01T10:24:57.736Z",
           "declaredArea": {
               "count": 2000.0
           },
           "auditedArea": null,
           "cropDetails": {
               "cropId": 2351,
               "cropName": "potatovar",
               "sowingDate": "2021-09-25T00:00:00Z",
               "expectedHarvestDate": "2027-03-18T00:00:00Z"
           }
       },
       {
           "id": 6801,
           "farmerCropId": 3,
           "name": "prod/CA-1",
           "createdDate": "2021-10-19T15:53:55.478Z",
           "lastModifiedDate": "2022-05-17T08:06:43.062Z",
           "declaredArea": {
               "count": 200.0
           },
           "auditedArea": null,
           "cropDetails": {
               "cropId": 2251,
               "cropName": "potatosub",
               "sowingDate": null,
               "expectedHarvestDate": null
           }
       },
       {
           "id": 7101,
           "farmerCropId": 4,
           "name": "ptest/CA-1",
           "createdDate": "2021-10-20T12:35:53.048Z",
           "lastModifiedDate": "2022-06-27T10:44:26.803Z",
           "declaredArea": {
               "count": 200.0
           },
           "auditedArea": null,
           "cropDetails": {
               "cropId": 2251,
               "cropName": "potatosub",
               "sowingDate": "2021-10-29T00:00:00Z",
               "expectedHarvestDate": "2024-07-25T00:00:00Z"
           }
       },
       {
           "id": 9302,
           "farmerCropId": 6,
           "name": "Seed Input B1/CA-1",
           "createdDate": "2021-11-03T10:09:13.517Z",
           "lastModifiedDate": "2022-06-27T10:44:26.839Z",
           "declaredArea": {
               "count": 555.0
           },
           "auditedArea": {
               "count": 0.4604579313344315
           },
           "cropDetails": {
               "cropId": 8801,
               "cropName": "Cherry ",
               "sowingDate": "2021-11-02T00:00:00Z",
               "expectedHarvestDate": "2022-01-31T00:00:00Z"
           }
       },
       {
           "id": 9301,
           "farmerCropId": 5,
           "name": "Seed Input B2/CA-1",
           "createdDate": "2021-11-03T10:09:13.387Z",
           "lastModifiedDate": "2022-06-27T10:44:26.845Z",
           "declaredArea": {
               "count": 77.0
           },
           "auditedArea": {
               "count": 0.20857188551652042
           },
           "cropDetails": {
               "cropId": 8801,
               "cropName": "Cherry ",
               "sowingDate": "2021-11-02T00:00:00Z",
               "expectedHarvestDate": "2022-01-31T00:00:00Z"
           }
       }
   ]

Get Satellite Details
---------------------

Parameters which can be passed as **kwargs or Optional Parameters
-----------------------------------------------------------------
Satellite details returns data for satellite indices and
crop details for the models subscribed.

        :param Ref ca_ids: Unique identifiers for plot/CA, e.g. ids=1234,5678

        :param str captured_date_time: Indicates timestamp when satellite insights processed, e.g. date = 2021-12-23T00:00:00Z

        :param str category: Cloud mask parameter.

        :param str max_cloud_coverage: Cloud coverage refers the fraction of sky covered with clouds, filters record where cloudCoverge <= maxCloudCoverage

        :param str min_cloud_coverage: Cloud coverage refers the fraction of sky covered with clouds, filters record where cloudCoverge >= minCloudCoverage

        :param str sort_by: Sort by given parameter name

        :param str order_by: Order the result in ascending or descending format. Default order is 'ASC'

         **MAX return size of response list is 5000**

.. code-block:: python

   import json
   import logging
   import urllib

   from python_sdk_client.cropin_api import CropinAPI

   satellite_response = cropin_api.get_satellite_details()
   print("satellite metrics with no filters :{}".format(satellite_response))

   #response
   [
     {
       "id": "61c9625536d002b6d6605b0c",
       "createdDateTime": "2021-12-27T06:51:01.706Z",
       "status": "active",
       "tenantType": "SMARTFARM_PLUS",
       "orgId": "test",
       "boundaryId": "61c2eb95cafeb94ef12496f9",
       "boundaryType": "PLOT",
       "capturedDateTime": "2021-12-15T00:00:00Z",
       "metrics": {
         "errorCodes": {
           "boundaryMetrics": "cmk"
         },
         "boundaryMetrics": {
           "cloudCoverage": null,
           "ndvi": null,
           "savi": null,
           "evi": null,
           "chire": null,
           "ndre": null,
           "arvi": null,
           "lswi": null,
           "lai1": null,
           "lai2": null,
           "rgiLow": null,
           "rgiMedium": null,
           "rgiHigh": null,
           "vis": null,
           "category": null
         },
         "cropMetrics": null
       }
     },
     {
       "id": "61e8ee51dc873a27e007ccb2",
       "createdDateTime": "2022-01-20T05:08:33.388Z",
       "modifiedDateTime": "2022-01-20T05:08:33.388Z",
       "status": "active",
       "tenantType": "SMARTFARM_PLUS",
       "orgId": "test",
       "boundaryId": "61e8ec4c09e1880458676b35",
       "boundaryType": "PLOT",
       "capturedDateTime": "2021-12-06T00:00:00Z",
       "metrics": {
         "errorCodes": {
           "cropMetrics": "No sowing date available"
         },
         "boundaryMetrics": {
           "cloudCoverage": 0,
           "ndvi": 0.44414854049682617,
           "savi": 0.6661359071731567,
           "evi": null,
           "chire": -0.7147309184074402,
           "ndre": 0.2688053250312805,
           "arvi": 0.3029395639896393,
           "lswi": 0.14890527725219727,
           "lai1": null,
           "lai2": null,
           "rgiLow": null,
           "rgiMedium": null,
           "rgiHigh": null,
           "vis": null,
           "category": null
         },
         "cropMetrics": []
       }
     },
     {
       "id": "61e8ee52d7a6a1c2d7d9af4f",
       "createdDateTime": "2022-01-20T05:08:34.988Z",
       "modifiedDateTime": "2022-01-20T05:08:34.988Z",
       "status": "active",
       "tenantType": "SMARTFARM_PLUS",
       "orgId": "test",
       "boundaryId": "61e8ec4c09e1880458676b35",
       "boundaryType": "PLOT",
       "capturedDateTime": "2021-12-11T00:00:00Z",
       "metrics": {
         "errorCodes": {
           "cropMetrics": "No sowing date available"
         },
         "boundaryMetrics": {
           "cloudCoverage": 7.575757575757578,
           "ndvi": 0.39165952801704407,
           "savi": 0.5874088406562805,
           "evi": null,
           "chire": -0.7646074891090393,
           "ndre": 0.2674875557422638,
           "arvi": 0.2688809931278229,
           "lswi": 0.06518805027008057,
           "lai1": null,
           "lai2": null,
           "rgiLow": null,
           "rgiMedium": null,
           "rgiHigh": null,
           "vis": null,
           "category": null
         },
         "cropMetrics": []
       }
     },
     {
       "id": "61e8ee60eab4ebc70e8799cf",
       "createdDateTime": "2022-01-20T05:08:48.933Z",
       "modifiedDateTime": "2022-01-20T05:08:48.933Z",
       "status": "active",
       "tenantType": "SMARTFARM_PLUS",
       "orgId": "test",
       "boundaryId": "61e8ec4c09e1880458676b35",
       "boundaryType": "PLOT",
       "capturedDateTime": "2021-12-16T00:00:00Z",
       "metrics": {
         "errorCodes": {
           "cropMetrics": "No sowing date available"
         },
         "boundaryMetrics": {
           "cloudCoverage": 78.78787878787878,
           "ndvi": 0.16200324892997742,
           "savi": 0.24297375977039337,
           "evi": null,
           "chire": -0.7676008939743042,
           "ndre": 0.12355568259954453,
           "arvi": 0.0990009680390358,
           "lswi": -0.16970780491828918,
           "lai1": null,
           "lai2": null,
           "rgiLow": null,
           "rgiMedium": null,
           "rgiHigh": null,
           "vis": null,
           "category": null
         },
         "cropMetrics": []
       }
     },
     {
       "id": "61e8ee6566d5c5658486c1da",
       "createdDateTime": "2022-01-20T05:08:53.392Z",
       "modifiedDateTime": "2022-01-20T05:08:53.392Z",
       "status": "active",
       "tenantType": "SMARTFARM_PLUS",
       "orgId": "test",
       "boundaryId": "61e8ec4c09e1880458676b35",
       "boundaryType": "PLOT",
       "capturedDateTime": "2021-12-21T00:00:00Z",
       "metrics": {
         "errorCodes": {
           "cropMetrics": "No sowing date available"
         },
         "boundaryMetrics": {
           "cloudCoverage": 30.303030303030297,
           "ndvi": 0.16759710013866425,
           "savi": 0.251361608505249,
           "evi": null,
           "chire": -0.6116514801979065,
           "ndre": 0.12325365841388702,
           "arvi": 0.09969054162502289,
           "lswi": -0.1600313037633896,
           "lai1": null,
           "lai2": null,
           "rgiLow": null,
           "rgiMedium": null,
           "rgiHigh": null,
           "vis": null,
           "category": null
         },
         "cropMetrics": []
       }
     }
   ]

Get Yield Details
---------------------

Parameters which can be passed as **kwargs
------------------------------------------

Fetches yield details for the plot ids passed.

        :param int ca_id: Unique identifier for plot/CA , e.g. id= 1234

        :param str order_by: Order the result in ascending or descending format. Default order is 'ASC'

        :param Ref page: Page represents page no. in a paginated response.Page starts from 0, valid page can be zero or a positive number.

        :param Ref size: Size represents the number of records that are displayed when a page loads,it can be between 10 to 300. Default size is 50.

        :param list[str] sort: Sorting criteria in the format: property(,asc|desc). Default sort order is ascending. Multiple sort criteria are supported.

        :param str sort_by: Sort the result based on given field/fields in natural sorting order (ASC). Maximum 2 fields are allowed.

        **MAX return size of response list is 5000**
.. code-block:: python


     import json
     import logging
     import urllib

     from python_sdk_client.cropin_api import CropinAPI

     yield_response = cropin_api.get_yield_details()
     print("yield data with no filter passed :{}".format(yield_response))

     #response

       [
        {
          "id": "623add7b5ae05f5b17276e64",
          "createdDateTime": "2022-03-23T08:42:35.299Z",
          "modifiedDateTime": "2022-03-23T08:44:26.099Z",
          "tenantType": "SMARTFARM_PLUS",
          "boundaryId": "61c3000f4fd59d34b0faf408",
          "externalId": "externalId_qa_a_160",
          "modelType": "ENERGYBALANCE",
          "orgId": "test",
          "crop": "Potato1",
          "cropVariety": "FL 2108",
          "predictionDate": "2021-01-29T18:30:00.000+00:00",
          "data": {
            "yieldMin": "219.209344",
            "yieldMax": "242.284011",
            "yieldAvg": "None",
            "plannedHarvestProjection": "123044.503811"
          }
        }
      ]


Get Weather Details
---------------------

Parameters which can be passed as **kwargs
------------------------------------------

Fetches weather details for the plot ids passed.

        :param int ca_id: Unique identifier for plot/CA , e.g. id= 1234

        :param str _date: Indicates timestamp when satellite insights processed, e.g. date = 2021-12-23T00:00:00Z

        :param str date_from: Filter records for specific date range e.g. dateFrom = 2021-12-23T00:00:00Z

        :param str date_to: Filter records for specific date range e.g. dateTo = 2021-12-23T00:00:00Z

        :param str order_by: Order the result in ascending or descending format. Default order is 'ASC'

        :param str sort_by: Sort the result based on given field/fields in natural sorting order (ASC). Maximum 2 fields are allowed.

         **MAX return size of response list is 5000**

.. code-block:: python

     import json
     import logging
     import urllib

     from python_sdk_client.cropin_api import CropinAPI

     weather_response = cropin_api.get_weather_details()
     print("weather data with no filter passed :{}".format(weather_response))

     #response

      [
        {
          "plotId": "61d6e5f8e7836149511145fc",
          "plotName": "Plot1",
          "externalId": "externalId",
          "date": "2022-03-31T07:02:23.059Z",
          "weather": {
            "precipitation": null,
            "dayTemperature": 33.824999999999996,
            "nightTemperature": 28.458333333333332,
            "dayRH": 44.666666666666664,
            "nightRH": null,
            "meanTemperature": null,
            "windSpeed": 9.320833333333333,
            "gdd": null,
            "diurnalTemperature": null
          },
          "gdd": {
            "cropStageName": "Sprouting",
            "gdd": null,
            "dd": null,
            "dayProgression": 1.12488928255093,
            "seasonProgression": null
          }
        }
      ]

Download Plot Image
-------------------

Parameters:
-----------
 Returns plot image byte streams for a single plot id at a given date and image type and name.

        :param int ca_id: Unique identifier for plot/CA , e.g. id= 1234 (required)

        :param str _date: Indicates captured satellite date in yyyy-MM-dd format, e.g. date=2022-03-15 (required)

        :param str image_name: Plot image name, e.g imageName = NDRE . (required)
           **Accepted Values -  CHI_Re, SAVI, NDRE, LAI2, NDVI, ARVI, LSWI, EVI, CROP_WATER_STRESS_LSWI, CROP_HEALTH_CROP_GREENESS, CROP_HEALTH_NITROGEN_UPTAKE, HLM**

        :param str image_type: Plot image type, e.g imageType = TIFF
           **Accepted Values - TIFF, PNG**

.. code-block:: python

     import json
     import logging
     import urllib

     from python_sdk_client.cropin_api import CropinAPI

     download_response = cropin_api.download_image(plot_id='62305d0110197fce8a2d7b40', image_name='HLM',
                                                  image_type='TIFF', date='2021-02-03')
     print("download_response is: {}".format(download_response))

     # code to convert the bytes to image
     imgdata = base64.b64decode(download_response['bytes'])
     filename = 'image.jpg'
     with open(filename, 'wb') as f:
        f.write(imgdata)

     #Request
      {
        "boundaryId": "62305d0110197fce8a2d7b40",
        "imageType": "TIFF",
        "imageName": "HLM",
        "date": "2021-02-03",
        "bytes": "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"
      }
.. include:: python_sdk_client.rst


.. toctree::
   :maxdepth: 2
   :caption: Contents:


Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
