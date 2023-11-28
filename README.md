import pandas as pd
import matplotlib.pyplot as plt
from mpl_toolkits.basemap import Basemap

# Specify the file path
file_path = "apt20200420_00_12.csv"

# Read the data into a DataFrame
data = pd.read_csv(file_path)

# Assuming your columns are named 'Latitude' and 'Longitude'
latitudes = data['30.872607']
longitudes = data['131.301985']

# Create a Basemap instance
plt.figure(figsize=(10, 8))
m = Basemap(projection='mill', llcrnrlat=latitudes.min(), urcrnrlat=latitudes.max(),
            llcrnrlon=longitudes.min(), urcrnrlon=longitudes.max(), resolution='c')

# Draw map components
m.drawcoastlines()
m.drawcountries()
m.drawmapboundary(fill_color='lightblue')
m.fillcontinents(color='lightgreen', lake_color='lightblue')

# Convert latitudes and longitudes to map coordinates
x, y = m(longitudes.tolist(), latitudes.tolist())

# Plot data points on the map
m.scatter(x, y, marker='o', color='red', zorder=5)

# Show the map
plt.title('Data plotted on map')
plt.show()


