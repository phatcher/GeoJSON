# BAMCIS GeoJSON
An implementation of GeoJSON written in .NET Core 2.0. The library complies with the requirements of RFC 7946 (https://tools.ietf.org/html/rfc7946).

## Usage

### Basic Example 1

Given some GeoJSON data, such as:

    {
      "type": "Feature",
      "geometry": {
        "type": "Point",
        "coordinates": [ 102.0, 0.5 ]
      },
      "properties": {
        "prop0": "value0"
      }
    }

You can receive the text and deserialize it to a GeoJSON object

    GeoJson data = JsonConvert.Deserialize<GeoJson>(jsonString);

Once the data is deserialized, you can cast it to its actual type

	switch (data.Type)
	{
		case GeoJsonType.Feature:
		{
            Feature feature = (Feature)data;
		    break;
		}
		...
	}

### Basic Example 2
If you know what kind of GeoJSON you're receiving, you can deserialize to it directly:

    FeatureCollection Col = FeatureCollection.FromJson(data);

And also go back to JSON data:

    string Json = Col.ToJson(Formatting.Idented);

### Basic Example 3

Or you can create a GeoJSON object and serialize it:

    Position Pos1 = new Position(100.0, 0.5);
	Position Pos2 = new Position(101.0, 1.0);
	MultiPoint Mp = new MultiPoint(new Position[] {Pos1, Pos2});
	string Json = JsonConvert.Serialize(Mp);

### Usage Notes

Each of the 9 GeoJSON types: **Feature**, **FeatureCollection**, **GeometryCollection**, **LineString**, **MultiLineString**, **MultiPoint**, **MultiPolygon**,
**Point**, and **Polygon** all have convenience methods ToJson() and FromJson() to make serialization and deserialization easy.

There are two additional types that can be used. A **LinearRing** is a LineString that is connected as the start and end and forms
the basis of a polygon. You can also use the abstract **Geometry** class that encompasses LineString, MultiLineString, MultiPoint, MultiPolygon,
Point, and Polygon.

The Feature **'Properties'** property implements an `IDictionary<string, dynamic>` in order to accomodate any type of property structure that may 
be sent.

## Revision History

### 1.0.0
Initial release of the library.
