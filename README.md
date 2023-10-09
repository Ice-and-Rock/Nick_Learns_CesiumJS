### Nick_Learns_CesiumJS
A sandbox to play with the CesiumJS Libraries

Testing for Github Repo


### Issues form CesiumJS.com
The following code block from the 'flight planner' doesn't work ❌
<code>
// Keep your `Cesium.Ion.defaultAccessToken = 'your_token_here'` line from before here. 
const viewer = new Cesium.Viewer('cesiumContainer', {
  terrain: Cesium.Terrain.fromWorldTerrain(),
});

const osmBuildings = await Cesium.createOsmBuildingsAsync();
viewer.scene.primitives.add(osmBuildings);
</code>

## Instead, use this... ✅
These code snippets are a breakdown of the file extensions *cesium world terrain* , *cesium OSM buildings* and *bing maps arial imagery* 

    Cesium World Terrain
        ~ With water Mask extension
    - fuses data sources into single quantized-mesh terrain tilesets for 3D visuals

    Cesium OSM Buildings
    - 3D building rendering derived from OpenStreetMap

    Bing Maps Arial
        ~ With 'labels' extension
    - world imagery for urban areas with down to 15cm resolution 

<code>
   Cesium.Ion.defaultAccessToken =
          "YOUR PASS KEY - Paste it here";
        const viewer = new Cesium.Viewer("cesiumContainer", {
            // 3D terrain render
          terrainProvider: Cesium.createWorldTerrain({
            requestWaterMask: true,
          }),
            // Bing world with labels
          imageryProvider: Cesium.createWorldImagery({
            style: Cesium.IonWorldImageryStyle.AERIAL_WITH_LABELS,
          }),
        });
        // 3D buildings render
        viewer.scene.primitives.add(Cesium.createOsmBuildings());
</code>

## Cartesian3.fromDegrees to convert Lat / Long / Height to X, Y & Z

<code>
// STEP 3 CODE (all points)
// These are all the radar points from this flight.
const flightData = JSON.parse(
    <!-- LAT, LONG & HEIGHT: API DATA-->
    );
// Create a point for each.
for (let i = 0; i < flightData.length; i++) {
  const dataPoint = flightData[i];

  viewer.entities.add({
    description: `Location: (${dataPoint.longitude}, ${dataPoint.latitude}, ${dataPoint.height})`,
    position: Cesium.Cartesian3.fromDegrees(dataPoint.longitude, dataPoint.latitude, dataPoint.height),
    point: { pixelSize: 10, color: Cesium.Color.RED }
  });
}
</code>