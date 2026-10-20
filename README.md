# EE292M_3a_HWcapstone plan

Why this is worth doing:
I-V curve analysis is crucial for determining LED characteristics. This data extraction could be done manually but is cumbersome and time consuming for me. It must be done faster so that I can gain insights on my devices sooner.

Milestones (I-V curve handler):
1) Button that allows a dialog to appear for someone to submit a folder to the backend
2) Visualizer (linear and log scale) that immediately extracts and graphs I-V curves for all CSVs contained in said folder. Legend only reads bare file names.
3) File identification algorithm for identifying which files belong to LEDs of different sizes, while still separating multiple LEDs of the same size (e.g. 100um_1 is different from 100um_2 is different from 100um_15, representing the first, second, and fifteenth measured devices).
4) Toggles near the I-V graphs that allow the user to select LEDs of which size to be graphed (e.g. only graph 100um LEDs, only graph 5um and 10um LEDs on the same graph, etc.).
5) Toggles that allow the user to select just one I-V curve to graph out of the full CSV list, organized by LED size
6) Elaborate on steps 3, 4, and 5, but with other repeat tags in the file names (e.g. SiO2passivated)
7) Ideality factor extraction for each LED in the backend
8) Visualization of ideality factor vs. voltage for each LED
9) Threshold voltage extraction for each LED in the backend
10) Highlighting of threshold voltage on the I-V curves (linear and logarithmic) using a dedicated, additional point on the graph.

Top risks:
Automatic identification of tags in .csv filenames may be problematic, especially if a filename contains extra information unique to just one device (defective, unique/unseen behavior, other marker). Consider a separate dialog where I can look at all the filenames in one place and then manually specify my own file tags.

Frontend vs. backend:
Backend should handle all ideality factor extraction and threshold voltage extraction. Frontend handles visualization and feeds the input file folder to the backend. Frontend is where the user submits the folder location for all the CSV files, and the backend 