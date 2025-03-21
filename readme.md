# Visualizing AgentTorch Simulations

This module provides a Python API that works seamlessly with AgentTorch
to visualize a simulation using the trajectory of its state.

The various supported types of visualizations are described below. To
request/add a new visualization, please open a pull request or an issue.

## GeoPlot

This visualization renders a 3-D plot of the data given the state
trajectory of a simulation, and the path of the property to render.

It generates an HTML file that contains code to render the plot using
Cesium Ion, and the GeoJSON file of data provided to the plot.

An example of its usage is as follows:

```py
from agent_torch.visualize import GeoPlot

# create a simulation
# ...

# create a visualizer
geoplot = GeoPlot(config, cesium_token)

# visualize in the runner-loop
for i in range(0, num_episodes):
  runner.step(num_steps_per_episode)

  geoplot.visualize(
    name = f"consumer-money-spent-{i}",
    state_trajectory = runner.state_trajectory,
    entity_position = "consumers/coordinates",
    entity_property = "consumers/money_spent",
  )
```
### 📌 Explanation of Parameters in `geoplot.visualize(...)`

| Parameter          | Description |
|-------------------|-------------|
| `name`  | A string specifying the **file name** for the generated GeoPlot visualization. |
| `state_trajectory` | The complete **state history** of the simulation. Used to track movement over time. |
| `entity_position` | The **path in the simulation state** where the entity’s coordinates (latitude, longitude) are stored. |
| `entity_property` | The **path in the simulation state** where the **property to visualize** is stored (e.g., money spent, distance traveled). |

🔹 **Example Use Case:**  
If you want to track how **consumers’ money spent** changes **over time** in the simulation,  
you will set `entity_property = "consumers/money_spent"`.  





