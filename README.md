#Backbone-MapStick

Two-way bindings between backbone models to google map overlays. Place your markers based on model properties or drag the marker to update the model, or both. Includes Marker, Infowindow, Polyline, Polygon, Rectangle, Circle and some useful overlay collection machinery.

Also supports the use of Drawing Manager to place or draw new bound elements.

The effect is to make your map elements _almost_ as easy to manage as your views.

Mapstick is almost completely undocumented, so good luck with that. Interface docs might appear here one day.

Modelled originally on Stickit but differs in that we don't have simple DOM bindings and have to provide a bit more interface.
The main difference is that we declare bindings with `modelChanged` and `overlayChanged` methods.

Mapstick has been in production use more or less unchanged for five years, so it's pretty strong but also a little
overdue for a service.


## Usage

    class Example.Overlays.InfoWindow extends MapStick.InfoWindow
      modelEvents:
        deselected: "close"
        remove: "close"
        hide: "close"

      bindings:
        position:
          lat: "lat"
          lng: "lng"


    class Example.Overlays.Marker extends MapStick.Marker
      defaultOptions:
        draggable: true
        raiseOnDrag: true
        zIndex: 40
        icon:
          path: google.maps.SymbolPath.CIRCLE
          scale: 15
          fillOpacity: 0.6
          fillColor: "#d1005d"
          strokeWeight: 0

      bindings:
        opacity:
          attributes: ["opacity", "selected"]
          modelChanged: "opacity"
        position:
          lat: "lat"
          lng: "lng"
        icon:
          attributes: ["icon_url", "category", "selected"]
          modelChanged: "markerIcon"
        zIndex: "z_index"
        visible:
          attribute: "visibility"
          modelChanged: "isVisible"

    class Example.Overlays.Markers extends MapStick.OverlayCollection
      itemView: Example.Overlays.Marker

      collectionEvents:
        hide: "hide"
        show: "show"



## Development

$ grunt

And that's it. Mapstick is a bit vintage now.

## Dependencies

- [Backbone.js](http://backbonejs.org/)
- [Google Maps API](https://developers.google.com/maps/documentation/javascript/)
