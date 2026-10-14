Follow AGENTS.md.

You are to develop a small containerized web app. This web app is intended to visualize data related to GaN LEDs, allowing for easy extraction and visualization of various components of the LED. It will be used by semiconductor researchers attempting to develop high-frequency, low-power LEDs for optical communication. The primary focus is on visualization for use in presentations and data extraction for the LEDs from measurements.

First, for easy cohesive visualization, the topmost section of the web app is intended to be an LED material stack visualization tool. The user can select the LED substrate material, LED buffer layer, number of quantum wells, quantum well compositions, electron blocking layer composition if relevant, and the thicknesses of all associated layers. Beside these inputs is a visualization showing the material stack, with the substrate on bottom and all other layers added on top, with thicknesses labeled beside the material stack. The diagram does not need to be to scale, but rather serves as a quick tool to describe the LED material structure without needing to painstakingly align rectangles manually in a PowerPoint presentation. Textboxes should allow users to title each layer as desired, and add new layers as they see fit, each with thicknesses, and arrow buttons should allow them to change the relative positioning of each layer.

In the section below, the user should be able to specify a folder, which the user will fill with .csv files containing data from LEDs that they have characterized. Each .csv file will come with a large header containing probe station settings, as well as columns reporting the voltage, current, and resistance measured for a given LED. Each .csv file will also contain information about the LED characterized, so that each current-voltage measurement can be correlated with a real device on a real chip. Once a user specifies a folder for the web app to look through, this section of the web app should perform the following:
1) Each .csv is a unique device. Looking at the title of each .csv, the device size should be extracted, which will commonly appear as "???um," where ??? is a number like 100, 50, or 5.
2) From each .csv, extract the current-voltage data for an LED of a known radius, as read from the file title. Units are amps and volts, respectively.
3) Plot the I-V curves on a linear scale and on a log scale in two separate graphs, side by side. Include toggles in the graph settings to show all devices present in the folder, show all devices of a given size (e.g. 50um, 25um), or show just one device of a given size that the user can then specifically select.
4) Calculate the threshold voltage of every LED. This should be done by calculating the second derivative of current with respect to voltage and determining where the first maximum of d^2I/dV^2 occurs. Label the threshold voltage as a point on each I-V curve as plotted above.
5) Calculate the ideality factor with respect to voltage for each LED; that is, at every voltage, measure the ideality factor n. It is to be calculated using the slope at each point and by taking into account the thermal voltage V_t, for which one can assume room temperature (T=293K). Use the formula n = (q/kT)*(d ln(I)/dV)^-1, where q is the electron charge and K is the Boltzmann constant. Graph this in yet another plot showing ideality factor n versus voltage.

There are several data exceptions to be wary of.
1) If a file title contains the word "REDO," ignore the file with an identical name but which does not contain "REDO." These are redone measurements due to cable issues, inconsistent contact quality, and more.
2) Ignore data inside of a .csv file where the probe station hits compliance. This occurs when the current reaches the maximum permitted current (typically 100 mA or 1 A), resulting in constant current as voltage changes. Compliance is hit when an LED could consume more current but the cables connecting it cannot provide more.
3) Expect multiple LEDs of the same size (e.g. multiple 100um LEDs) to be measured. Each will have some unique identifier to distinguish multiples of LEDs in the .csv filename; for example, multiple LEDs of size 100um may be labeled _1, _2, _3, etc.
4) Other tags may be included, including specific labels for whether a chip was passivated or not, whether an LED was fabricated on a GaN substrate or a sapphire substrate, etc. Keep track of these elements in the file name as identifiers for each LED fabricated. For example, "100um_SiO2passivated_1" will be distinct device from "100um_Al2O3passivated_1" and should appear as a separate I-V curve on the aforementioned visualization, with its own label in the graph legend. If a tag appears twice or more, it should also appear as a toggle for whether it should be graphed (i.e. only graph all I-V curves that contain "SiO2passivated" in their filename).

There are several checks that should be done to verify the extracted data.
1) Threshold voltage is commonly between 2.4 and 3 volts. If the extracted threshold voltage of an LED is lower or higher than this limit, flag it and highlight the file in a dialog beneath this section of the web app.
2) Ideality factor should never be less than 1. If it is less than one, flag the file in the same was as in item 1 here.

Additionally, reject any Excel files present in the folder. Ignore any PNGs in the folder.

This is a Dockerized, containerized project. Inside of the folder provided for you in this project, you will find docker-demo-example, which contains an extremely basic but functional web app. Follow its general Dockerization procedure.

## Rules
- Run code and tests through `make`, not directly on the laptop.
- Keep changes small; update/add a test for each change.
- Do not edit the Dockerfile unless asked.