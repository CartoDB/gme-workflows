### Upload and style vector data for viewing on the web

A vector file defines geographic features: points, lines and polygons. See the topic on [http://docs.cartodb.com/cartodb-editor.html#supported-file-formats](supported formats) in the CartoDB Documentation.

API workflow in brief:

- Upload the vector data along with the associated sidecar files in a zip file by using the [CartoDB Editor](http://docs.cartodb.com/cartodb-editor.html) or making a request to the [Import API](http://docs.cartodb.com/cartodb-platform/import-api.html) directly. ([Supported formats](http://docs.cartodb.com/cartodb-editor.html#supported-file-formats).)
- Go to the CartoDB Editor (<YOUR_USERNAME>.cartodb.com) and open the new table.
- Style the data by [configuring a wizard](http://docs.cartodb.com/tutorials/visualization_wizard.html) or by manually [editing the CartoCSS](http://docs.cartodb.com/tutorials/conditional_styling.html).
- Set the table's [privacy settings](http://docs.cartodb.com/cartodb-editor.html#table-privacy-settings) to determine who can see it.
- Create a new visualization by clicking the _visualize_ button in the top right corner of the CartoDB Editor and enter a name.
- Share your visualization by clicking the _share_ button in the top right corner of the CartoDB Editor and use one of the given options (Get the link, embed it, or use [CartoDB.js](http://developers.cartodb.com/documentation/cartodb-js.html)).

Try it yourself by following [the example](http://docs.cartodb.com/cartodb-platform/import-api.html#uploading-a-local-file) in the Import API documentation.


### Insert vector data incrementally

Instead of uploading all the features at once via a file upload, as described in the above vector-upload scenario, you can insert new date over time / as needed.

This workflow is useful when your application needs to collect data or offers a user interface where people can add features, for example.

API workflow in brief:

- Create a new empty table in the [CartoDB Editor](http://docs.cartodb.com/cartodb-editor.html).
- Navigate to your new table
- Using the column headers, create any new columns that you need and set their data types.
- Copy your API key. ([Find your API key](http://docs.cartodb.com/cartodb-editor.html)).
- Add features via the [CartoDB SQL API](http://docs.cartodb.com/cartodb-platform/sql-api.html).

You can interact with the CartoDB SQL API directly with REST calls, or use one of the official [client libraries](http://docs.cartodb.com/cartodb-platform/sql-api.html#libraries-in-different-languages). Here's an example of inserting a point into a table with the [python client library](https://github.com/Vizzuality/cartodb-python):

```
from cartodb import CartoDBAPIKey, CartoDBException

API_KEY ='YOUR_CARTODB_API_KEY'
cartodb_domain = 'YOUR_CARTODB_DOMAIN'
cl = CartoDBAPIKey(API_KEY, cartodb_domain)
try:
   print cl.sql("insert into mytable (the_geom,foo,bar) values (CDB_LatLng(40.7127,-74.0059),'testing',123)")
except CartoDBException as e:
   print ("some error ocurred", e)

```

### Upload imagery

A raster image is a geo-referenced image. CartoDB supports GeoTIFF images. See the topic on [http://docs.cartodb.com/cartodb-editor.html#supported-file-formats](supported formats) in the CartoDB Documentation.

API workflow in brief:

- Upload the vector data along with the associated sidecar files in a zip file. ([Supported formats](http://docs.cartodb.com/cartodb-editor.html#supported-file-formats).)
- Go to the CartoDB Editor (<YOUR_USERNAME>.cartodb.com).
- You will see a new _Raster Table_ item in your table list. Currently, you can only interact with images in CartoDB over the SQL API, i.e., you won't be able view your GeoTIFF in the CartoDB Editor.

For the import, follow [the example](http://docs.cartodb.com/cartodb-platform/import-api.html#uploading-a-local-file) in the Import API documentation. Here's [an example](http://bl.ocks.org/rochoa/d3cf809120bda97d0826) of creating a map with a CartoDB Raster Table and CartoDB.js.

For smaller images or small sets of images, using the Google Maps API to create a [ground overlay(s)](https://developers.google.com/maps/documentation/javascript/examples/groundoverlay-simple) with the image(s) is often easier.

### Upload and process large volumes of imagery












