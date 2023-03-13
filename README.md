# cesiumTest

// Wait for the tileset to load before checking for intersection
tileset.readyPromise.then(function() {
  
    var intersects = false;

    // Get the positions of the polyline
    var positions1 = entity.polyline.positions.getValue(Cesium.JulianDate.now());

    // Check if any of the polyline segments intersect the tileset
    for (i = 0; i < positions1.length - 1; i++) {
      var start = positions1[i];
      var end = positions1[i + 1];
      var ray = new Cesium.Ray(start, Cesium.Cartesian3.subtract(end, start, new Cesium.Cartesian3()));
      console.log(tileset.boundingSphere);
      var intersection = Cesium.IntersectionTests.rayEllipsoid(ray, tileset.boundingSphere);

      
      if (intersection) {
        intersects = true;
        break;
      }
    }

    if (intersects) {
      console.log("The polyline intersects the tileset");
    } else {
      console.log("The polyline does not intersect the tileset");
    }
}).catch(function(error) {
  console.log(error);
});
