.. Insights SDK documentation master file, created by
   sphinx-quickstart on Wed Jun 29 10:41:49 2022.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to Insights SDK's documentation!
========================================

.. include:: install.rst

===========
Insights SDK
===========

Insights SDK has functions to fetch plots, satellite, weather and yield details.

It also exposes the plot image download function.

QUICKSTART
----------

.. code-block:: python

  import json
  import logging
  import urllib

  from python_sdk_client.clients_enum import EnvType
  from python_sdk_client.cropin_api import CropinAPI

  """Example on how to use CropAPI.
  """
  if __name__ == '__main__':
    logging.info(">>>>>>>>>>>> starting")
    cropin_api = CropinAPI("test", "12121212", "password", EnvType.QA)
    print(cropin_api)

    api_response = cropin_api.get_plot_details(plot_ids=None, org_id='test')
    print(api_response)

    sattelite_response = cropin_api.get_satellite_details(plot_ids=None, org_id='test')
    print(sattelite_response)

    weather_api = cropin_api.get_weather_details(plot_ids=None, org_id='test')
    print(weather_api)

    yield_response = cropin_api.get_yield_details(plot_ids=None, org_id='test')
    print(yield_response)


Authentication
----------------

.. code-block:: python

  import json
  import logging
  import urllib

  from python_sdk_client.clients_enum import EnvType

  cropin_api = CropinAPI("XXXX", "xyz", "xyz", EnvType.QA)

Error Codes -
-----------
For Invalid Credentials,
.. code-block:: python
   #Exception when calling AuthenticateApi->get_token: (404)

   {
   "timestamp": "2022-07-06T04:21:52.563Z",
   "status": 404,
   "error": "XXXX" : tenant not found",
   "errorCode": "404 NOT_FOUND"
   }

Get Plot Details
----------------
.. code-block:: python

   import json
   import logging
   import urllib

   from python_sdk_client.clients_enum import EnvType

   boundary_api = cropin_api.get_plot_details(plot_ids=None)
   print(boundary_api)


   #respnse
   [
   {
    "id": "62b3f6f0801da0763f661d58",
    "createdDateTime": "2022-06-23T05:15:26.333Z",
    "modifiedDateTime": "2022-06-23T05:15:26.333Z",
    "status": "active",
    "properties": {
      "geometry": {
        "type": "Point",
        "coordinates": [
          17.4553074,
          78.5477343
        ]
      },
      "type": "Feature",
      "properties": {
        "shape": "Circle",
        "radius": 1000
      }
    },
    "tenantType": "SMARTFARM_PLUS",
    "orgId": "test",
    "name": "test1",
    "type": "PLOT",
    "coordinates": {
      "type": "Polygon",
      "coordinates": [
        [
          [
            17.500601520815515,
            78.547730816062
          ],
          [
            17.49002200135015,
            78.55351298236255
          ],
          [
            17.463178649061778,
            78.55659078376468
          ],
          [
            17.432645129897583,
            78.55552178199157
          ],
          [
            17.412733566032554,
            78.5508070838242
          ],
          [
            17.412756123724797,
            78.54465536338589
          ],
          [
            17.4326755218177,
            78.53994507603842
          ],
          [
            17.46316664635189,
            78.53887760612797
          ],
          [
            17.489987440948024,
            78.54195152871866
          ],
          [
            17.500601520815515,
            78.547730816062
          ]
        ]
      ]
    },
    "geohash": "ec716a6aa3ec4a2724deece6c60f5c1d",
    "areaInHectares": 0.0011782487202325678,
    "externalId": "test3-June9",
    "tileDetails": {
      "SENTINEL": [
        "33XWH"
      ]
    },
    "cropDetails": [
      {
        "id": "219",
        "crop": "corn",
        "sowingDate": "2022-01-12T00:00:00.000+00:00",
        "harvestDate": null
      }
    ]
   },
   {
    "id": "62a83c79ea73816ce035e054",
    "createdDateTime": "2022-06-14T07:44:57.034Z",
    "modifiedDateTime": "2022-06-14T07:44:57.034Z",
    "tenantType": "SMARTFARM_PLUS",
    "orgId": "test",
    "name": "test1",
    "type": "PLOT",
    "coordinates": {
      "type": "Polygon",
      "coordinates": [
        [
          [
            73.81301879882812,
            19.23206673568465
          ],
          [
            73.93936157226562,
            19.23206673568465
          ],
          [
            73.93936157226562,
            19.2528118348149
          ],
          [
            73.81301879882812,
            19.2528118348149
          ],
          [
            73.81301879882812,
            19.23206673568465
          ]
        ]
      ]
    },
    "geohash": "464dd820dac2cebda60f53e1bdebbde3",
    "areaInHectares": 0.0026209933593514885,
    "externalId": "test_dec19",
    "tileDetails": {
      "SENTINEL": [
        "43QCB"
      ]
    },
    "cropDetails": [
      {
        "id": "219",
        "crop": "corn",
        "sowingDate": "2020-10-12T00:00:00.000+00:00",
        "harvestDate": null
      }
    ]
   },
   {
    "id": "62a83d0d338cd219c9e1264f",
    "createdDateTime": "2022-06-14T07:47:25.055Z",
    "modifiedDateTime": "2022-06-14T07:47:25.055Z",
    "tenantType": "SMARTFARM_PLUS",
    "orgId": "test",
    "name": "test1",
    "type": "PLOT",
    "coordinates": {
      "type": "Polygon",
      "coordinates": [
        [
          [
            73.81301879882812,
            19.23206673568465
          ],
          [
            73.93936157226562,
            19.23206673568465
          ],
          [
            73.93936157226562,
            19.2528118348149
          ],
          [
            73.81301879882812,
            19.2528118348149
          ],
          [
            73.81301879882812,
            19.23206673568465
          ]
        ]
      ]
    },
    "geohash": "464dd820dac2cebda60f53e1bdebbde3",
    "areaInHectares": 0.0026209933593514885,
    "externalId": "test_june14",
    "tileDetails": {
      "SENTINEL": [
        "43QCB"
      ]
    },
    "cropDetails": [
      {
        "id": "219",
        "crop": "corn",
        "sowingDate": "2020-10-12T00:00:00.000+00:00",
        "harvestDate": null
      }
    ]
   }
   ]

Get Satellite Details
---------------------

.. code-block:: python

   import json
   import logging
   import urllib

   from python_sdk_client.clients_enum import EnvType

   sattelite_response = cropin_api.get_satellite_details(plot_ids=None, org_id='test')
   print(sattelite_response)

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

.. code-block:: python


     import json
     import logging
     import urllib

     from python_sdk_client.clients_enum import EnvType

     yield_response = cropin_api.get_yield_details(plot_ids=None, org_id='test')
     print(yield_response)

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




.. include:: python_sdk_client.rst


Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
