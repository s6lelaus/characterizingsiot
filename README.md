# Setup
- You need to have MobVis installed as well as all of its packages and include the **build** and **mobvis** folders when using it. You can get MobVis from [this repository](https://github.com/lucNovais/MobVis/). Additionally, you need the [**networkx** package](https://networkx.org/).
- Add **your** directory with the SIoT mobility trace into the **traces** folder 
- Now add the **MobFixHumanNodesRemoved.ipynb** file to **your** trace
- Make sure MobVis can be used by also adding **build** and **mobvis** to the trace's folder
- Your folder hierarchy should look like this: 
```` 
./
build/
mobvis/
traces/
├─ YOUR_TRACE/
│  ├─ build/
│  ├─ mobvis/
│  ├─ contacts_trace.csv
│  ├─ home_locations.csv
│  ├─ info.csv
│  ├─ pos_trace.csv
│  ├─ sim-config.cfg
│  ├─ MobFixHumanNodesRemoved.ipynb
````


# How to clean the data from the SIoT mobility model
To get rid of the human nodes in the SIoT trace you need to have the **MobFixHumanNodesRemoved.ipynb in the folder of  your trace**. To use the script run it with the **trace's folder as the cwd**. It removes the human nodes, fixes the IDs of the other nodes, and initializes nodes that did not produce a single GPS point to their respective home location. 

After that edit the **tracename** variable in the **second cell** in **MobInt.ipynb** to match the name of your trace. Now have the **root folder as the cdw** and run the script. It will interpolate the low mobility nodes and append them to original fixed trace. As a result, you get  **pos_traceAddedZerosAndFixedAndLowsInterpolatedNaNRemoved.csv** which is the pos_trace parsed, initialized, interpolated and with correct IDs. This is the pos_trace one can work with.

Finally, you can use the **dedupContacts.ipynb** script to eliminate the duplicates and humans in the mobility model's contacts_trace. The resulting **contacts_traceNoHumansNoDupsFixed.csv** implicitly has the correct IDs.

When the scripts are run they generate some redundant files for debugging.

# Metric extraction

To extract the common metrics by MobVis, adjust the parameters in **extractAllMetrics.ipynb**. You also need to  add your trace's name to the **traceNames** dictionary in the second cell. Make sure that the ID in **traceToAnalyze** is corresponding to your trace.
When extracting the metrics for the first time, make sure to set the variables to **True** in **readFile** and **toSave**. The script will create a **cached** and **metrics** folder in your trace, which contains the cached and the metric dataframes.

The contact groups can be extracted with the code given in **contactgroups.ipynb**. 

# Plotting
The data for the metrics is given in the **metrics** folder. One can use the plotting functionality from MobVis or a plotting engine of your choice to visualize the data. 

# References 

da Silva, Lucas & Rettore, Paulo & Mota, Vinícius & Pereira, Bruno. (2022). MobVis: A Framework for Analysis and Visualization of Mobility Traces. 10.1109/ISCC55528.2022.9912988. 
Repository: https://github.com/lucNovais/MobVis/

Alves, Talita & Rettore, Paulo & Santos, Bruno. (2023). A Mobility Model of The Internet of Things. 221-229. 10.1145/3617023.3617054. 
Repository: https://github.com/talitaester/SIOT-MM-implementations (outdated, do not use)
