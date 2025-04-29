# 🏙️ **Street Local Closeness-Centrality Visualization with Momepy** 🏙️

This project visualizes **local street network closeness-centrality** for **Mashhad, Iran** using the **Momepy** library. Closeness-centrality is a measure of how close a node (street intersection) is to all other nodes in the network. This visualization helps identify key locations within a street network that are well-connected to other locations.

For more information on Momepy, visit [Momepy Documentation](http://docs.momepy.org/).

---

## 🚀 **Key Features**

- **Closeness-Centrality Calculation**: Use the **Momepy** library to calculate closeness-centrality for street intersections within a given radius.
- **OSM Data**: Data is sourced from **OpenStreetMap** (OSM) using **OSMnx** to extract the street network for the area of interest.
- **Closeness Centrality Visualization**: Visualize closeness-centrality using color gradients and Fisher-Jenks classification.
- **Basemap Integration**: Add a **contextual basemap** using **Contextily** to give spatial context to the closeness-centrality plot.
- **Scalebar**: Add a **scalebar** to the map for better spatial reference.

---

## 🧑‍🔬 **Getting Started**

### 1. **Install Required Libraries**

Ensure that you have the necessary libraries installed:

```bash
pip install geopandas momepy osmnx matplotlib contextily matplotlib-scalebar
```

### 2. **Run the Script**

1. **Open the Script**: Open the provided script in your preferred Python editor.
2. **Execute the Script**: Run the script to fetch the street network data for **District 6, Mashhad, Iran**, calculate **local closeness-centrality**, and generate the visualization.

---

## 🔧 **How It Works**

### 1. **Import Libraries**

The script imports essential libraries like **GeoPandas**, **Momepy**, **OSMnx**, **Matplotlib**, and **Contextily**:

```python
import geopandas as gpd
import momepy
import osmnx as ox
import matplotlib.pyplot as plt
import matplotlib as mpl
import contextily
from matplotlib_scalebar.scalebar import ScaleBar
```

### 2. **Fetch Data from OpenStreetMap**

The script uses **OSMnx** to extract the street network data for **District 6, Mashhad, Iran**:

```python
streets_graph = ox.graph_from_place('District 6, Mashhad, Iran', network_type='drive')
streets_graph = ox.projection.project_graph(streets_graph)
```

The network is converted into **GeoDataFrames** for both **nodes** and **edges**.

### 3. **Closeness-Centrality Calculation**

The **Momepy** library is used to calculate **closeness-centrality** for each street intersection within a radius of 400 meters. This is done using the `closeness_centrality()` function from **Momepy**:

```python
primal = momepy.gdf_to_nx(edges, approach='primal')
primal = momepy.closeness_centrality(primal, radius=400, name='closeness400', distance='mm_len', weight='mm_len',legend=True)
```

### 4. **Visualization of Closeness-Centrality**

The closeness-centrality values are visualized using **matplotlib** and **GeoPandas**. The map is colored using the **Spectral_r** color palette and classified using the **Fisher-Jenks classification**:

```python
nodes.plot(ax=ax, column='closeness400', cmap='Spectral_r', scheme='quantiles', k=15, alpha=0.6)
```

### 5. **Adding Basemap and Scalebar**

A **dark basemap** from **Contextily** is added for better context, and a **scalebar** is included for spatial reference:

```python
contextily.add_basemap(ax, crs=nodes.crs, source=contextily.providers.CartoDB.DarkMatterNoLabels)
scalebar = ScaleBar(1, box_alpha=0, location="lower right", color='white', length_fraction=0.25, font_properties={"size": 12})
ax.add_artist(scalebar)
```

### 6. **Plot the Final Map**

The map is rendered, showing **closeness-centrality** values for the street intersections, with a **scalebar** for spatial reference.

### 7. **Save the Output**

You can save the final output as a **PNG** image for future reference:

```python
# Save the final plot as PNG
f.savefig("closeness_centrality_mashhad.png", dpi=300)
```

---

## 📊 **Outputs**

- **Closeness-Centrality Map**: A visualization of the **local closeness-centrality** for street intersections in **District 6, Mashhad**.
- **Basemap**: A **dark basemap** for spatial context.
- **Scalebar**: A **scalebar** added to the map for reference.

---


## 📈 **Future Enhancements**

- **Expanded Analysis**: Extend the analysis to other neighborhoods or cities to compare the closeness-centrality of different street networks.
- **Interactive Maps**: Use interactive map libraries like **Folium** or **Plotly** to allow users to explore the map interactively.
- **Other Centrality Measures**: Incorporate other centrality measures like **betweenness** or **degree centrality** to enhance the analysis.

---
![closeness_mhs](https://github.com/user-attachments/assets/6db683f7-440b-45ed-b6dd-ca145892a238)

