# node-gdal
[![NPM version](http://img.shields.io/npm/v/gdal.svg?style=flat)](https://www.npmjs.org/package/gdal)
[![Installs](http://img.shields.io/npm/dm/gdal.svg?style=flat)](https://www.npmjs.org/package/gdal)
[![Build Status](https://travis-ci.org/naturalatlas/node-gdal.svg)](https://travis-ci.org/naturalatlas/node-gdal)
[<img src="https://ci.appveyor.com/api/projects/status/mo06c2r5opdwak95?svg=true" height="20" alt="" />](https://ci.appveyor.com/project/brianreavis/node-gdal)

Read and write raster and vector geospatial datasets straight from [Node.js](http://nodejs.org) with this native [GDAL](http://www.gdal.org/) binding. GDAL [2.0.1](http://trac.osgeo.org/gdal/wiki/Release/2.0.1-News) ([GEOS](http://trac.osgeo.org/geos/) [3.4.2](http://trac.osgeo.org/geos/browser/tags/3.4.2/NEWS), [Proj.4](http://trac.osgeo.org/proj/) [4.8.0](http://www.osgeo.org/node/1268)) comes bundled, so node-gdal will work straight out of the box. To get started, browse the [**API Documentation**](http://naturalatlas.github.io/node-gdal/classes/gdal.html) or [examples](examples/).

```sh
$ npm install gdal --save
```

To link against shared libgdal, install using:

```sh
# requires libgdal-dev (debian: sudo apt-get install libgdal-dev)
$ npm install gdal --build-from-source --shared_gdal
```

## To publish
```js
npm adduser --registry https://npm.amristar.com
npm publish --registry https://npm.amristar.com
```

## Sample Usage

#### Raster
```js
var gdal = require("gdal");
var dataset = gdal.open("sample.tif");

console.log("number of bands: " + dataset.bands.count());
console.log("width: " + dataset.rasterSize.x);
console.log("height: " + dataset.rasterSize.y);
console.log("geotransform: " + dataset.geoTransform);
console.log("srs: " + (dataset.srs ? dataset.srs.toWKT() : 'null'));
```
#### Vector
```js
var gdal = require("gdal");
var dataset = gdal.open("sample.shp");
var layer = dataset.layers.get(0);

console.log("number of features: " + layer.features.count());
console.log("fields: " + layer.fields.getNames());
console.log("extent: " + JSON.stringify(layer.extent));
console.log("srs: " + (layer.srs ? layer.srs.toWKT() : 'null'));
```

## Notes

- This binding is *not* async, so it will block node's event loop. Be very careful (or avoid) using it in server code. We recommended using tools like [worker-farm](https://www.npmjs.com/package/worker-farm) to push expensive operations to a seperate process.

## Contributors

This is a fork of [node-gdal] (https://github.com/naturalatlas/node-gdal) provided by [Natural Atlas](https://github.com/naturalatlas) and [Mapbox](https://github.com/mapbox). Its contributors are [Brandon Reavis](https://github.com/brandonreavis), [Brian Reavis](https://github.com/brianreavis), [Dane Springmeyer](https://github.com/springmeyer), [Zac McCormick](https://github.com/zhm), and [others](https://github.com/naturalatlas/node-gdal/graphs/contributors).

## License

Copyright &copy; 2015–2017 [Natural Atlas, Inc.](https://github.com/naturalatlas) & [Contributors](https://github.com/naturalatlas/node-gdal/graphs/contributors)

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at: http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.
