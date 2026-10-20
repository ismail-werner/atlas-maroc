# Atlas Maroc

A free, single-file route planner for Morocco. Open `index.html` in a browser. No server, account or API key needed.

## Use it

- Tap cities on the map, or type a name. First is the start, last is the destination, anything between is a stop.
- Pick **Fastest**, **Shortest** or **No toll**.
- The side panel shows distance, drive time, an approximate toll in MAD and a step-by-step itinerary.
- **Watch the search** animates the cities the algorithm examines. **Turbo (A\*)** turns the straight-line guess on or off so you can compare.

## How it works

- The road network is a graph of about 44 cities and 90+ roads (autoroutes, national roads, mountain passes, desert roads) defined at the top of the script (`C` for cities, `E` for roads).
- Routes are found with Dijkstra's algorithm on a binary-heap priority queue. Turbo adds an A* heuristic (haversine distance divided by top speed), which never overestimates, so it returns the same best route while exploring fewer cities.
- Open `index.html?test` to run a self-check: A* must match plain Dijkstra on every city pair in every mode. The tab title shows `check OK` when it passes.
- Road-following lines are drawn from the public OSRM demo server. If it is unreachable, the route falls back to a dotted straight line. The route choice and the numbers are always computed locally.

## Accuracy

Distances are the straight-line distance times a factor per road type, and times use one average speed per type. Toll is roughly 0.35 MAD/km. It is an estimate for planning, not street-level navigation, and it does not know about traffic or closures. To improve it, add cities and roads to `C` and `E`, or import a real road network from OpenStreetMap.

## Map tiles

Tiles come from Esri World Street Map, which works when the page is opened from a file. OpenStreetMap's own tile server blocks file-based pages, but works if you host the page (for example on GitHub Pages). To switch, change the `L.tileLayer(...)` line.

## Credits

Map data © OpenStreetMap contributors. Tiles © Esri. Built with [Leaflet](https://leafletjs.com).
