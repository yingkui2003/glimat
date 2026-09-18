# GLIMAT: a QGIS plugin for glacier lineation and ice margin analysis
GLIMAT (Glacier Lineation and Ice Margin Analysis Toolkit) is a comprehensive QGIS plugin that integrates five complementary validation tools into a single, user-friendly interface: (1) APCA (Automated Proximity and Conformity Analysis) for ice margin offset comparison; (2) AFDA (Automated Flow Direction Analysis) for comparing modeled and observed flow directions; (3) LALA (Likelihood of Accordant Lineations Analysis) to quantify the likelihood of a glacier or ice sheet simulation aligning with the location and direction of observed glacial lineations; (4) APOA (Automated Polygon Overlap Analysis) for calculating F1‑score, IoU (Intersection over Union), precision, and recall between modeled ice extent and field‑mapped ice extent polygons; and (5) STPC (Surface/Thickness Point Comparison) for validating modeled ice surface elevation or thickness against field measurements at specific point locations. GLIMAT natively handles NetCDF files (one of the most common glacial model output formats), supports moving time windows for temporal smoothing, offers parallel processing for computational efficiency, and generates publication-ready visualizations. 

A test dateset for this plugin can be downloaded from https://zenodo.org/records/22836601.

# Installation Instructions
## In Windows:

### 1. Install QGIS (>3.22)
Download and install QGIS from the official website: https://qgis.org/download/

### 2. Open OSGeo4W Shell
#### Option A (Run as Administrator):
- Right-click on OSGeo4W Shell (from the QGIS installation folder)
- Select "Run as administrator"

If you cannot see the "Run as administrator" option directly in the Start Menu:
- Right-click on "OSGeo4W Shell" and select "Open file location".
- In the folder that opens, right-click the "OSGeo4W Shell" shortcut again and select "Run as administrator"

#### Option B:
If your account has administrator privileges, simply open OSGeo4W Shell from the Start Menu

**Note: Running as administrator is required to install Python packages.**

### 3. Install Python Libraries

#### Step 1: Update pip (Recommended)
```bash
python -m pip install --upgrade pip
```
#### Step 2: Install Required Libraries
```bash
python -m pip install numpy scipy pandas geopandas shapely rasterio xarray matplotlib pyproj netCDF4 cftime
```
**Note: You can omit python -m and use pip directly**
```bash
pip install numpy scipy pandas geopandas shapely rasterio xarray matplotlib pyproj netCDF4 cftime
```

### 4. Troubleshooting Common Issues

#### Rasterio installation issues
This plugin require rasterio 1.4.3 or lower for reading TIF and ASC files. you encounter errors related to rasterio, you may need to install an older version:

```bash
python -m pip install “rasterio<1.4.4”
```

#### NumPy version conflicts or compatibility issues
The plugin in QGIS4 works for numpy version of > 2.0. If you use lower versions, you may need to 
downgrade numpy to 1.26.4

```bash
python -m pip install “numpy<2.0”
```

#### Check installed versions
To check what libary versions you have installed:

```bash
python -m pip list
```

#### Force reinstall
If you have conflicting versions, force reinstall with specific versions (example):
```bash
python -m pip install --force-reinstall "numpy>=1.24.0,<2.3.0"
```

### 5. Additional Notes
**Existing Libraries**: If you already installed some of these libraries for other QGIS plugins, the plugin may encounter errors due to **version conflicts**. Reinstall the libraries with the specified versions if needed.
**QGIS crash**: IF QGIS keeps crashing when running this plugin, you may need to remove the QGIS in your computer and reinstall it again.

## In MacOS

### 1. Open Terminal on Mac/Linux. The bash window will show up.

Install Conda: If you haven't already, download and install Miniconda or Anaconda for macOS: https://www.anaconda.com/docs/getting-started/miniconda/install/mac-cli-install.

### 2. Create a New Environment: Open your terminal and create an environment specifically for QGIS.

```bash
conda create --name qgis_env python=3.12
```

**Note**: You can replace qgis_env with any name you prefer.

### 3. Activate the Environment:
```bash
conda activate qgis_env
```

### 4. Install python libraries:
```bash 
conda install -c conda-forge numpy scipy pandas geopandas shapely rasterio xarray matplotlib pyproj netCDF4 cftime
```

### 5. Install QGIS: Use the community-maintained conda-forge channel to install QGIS.
```bash
conda install -c conda-forge qgis
```

### 6. Run QGIS:
```bash
qgis 
```

**Note: If errors arise due to version conflicts (most commonly with numpy or rasterio), please refer to the troubleshooting section for Windows.**

## Install the Q_ACME plugin in QGIS
- Open QGIS
- Click the “Plugins” menu and click “Manage and install Plugins…”
- In the Plugins dialog, click Install from ZIP on the left panel. 
- Browse the Q_ACME_plugin.zip file and install the plugin. 

The “GLIMAT” plugin will be added to the “Plugins” menu and on the Toolbar.

The screenshot below shows how to install the plugin from the ZIP file: 1) click "Install from ZIP" on the left panel; 2) select the ZIP file; and 3) install the plugin and wait for the installation to complete.
<img width="1077" height="726" alt="image" src="https://github.com/user-attachments/assets/75472e6f-3b3e-4dd6-985a-19cece01a57f" />


If the installation is successful, run the GLIMAT plugin and you will see the interface below: 
<img width="975" height="951" alt="image" src="https://github.com/user-attachments/assets/2c0e4d46-3a41-46fd-9209-422197f6ac38" />

## Troubleshooting: QGIS Freezes or Displays "Not Responding" during ZIP Installation

If QGIS freezes when clicking "Install from ZIP", it usually means a required Python dependency is missing or there is a still permission issue in Windows.

#### Solution A (Recommended):
- Close QGIS forcefully via Task Manager (Ctrl + Shift + Esc).
- Open OSGeo4W Shell as Administrator.
- Make sure all required libraries are installed (see previous steps).
- Reopen QGIS as Administrator and try "Install from ZIP" again.

#### Solution B (Manual Installation):
- Extract (unzip) GLIMAT_plugin.zip.
- Copy the unzipped "GLIMAT_plugin" folder directly into your QGIS plugins directory:
%APPDATA%\QGIS\QGIS3\profiles\default\python\plugins\ or %APPDATA%\QGIS\QGIS4\profiles\default\python\plugins\ depending on your QGIS version.
- Open QGIS, go to Plugins → Manage and Install Plugins → Installed, and enable GLIMAT.

#### Verify Installation
To verify that all libraries are installed correctly, open QGIS and:
- Go to Plugins → Manage and Install Plugins
- Select Installed tab
- Find GLIMAT in the list
- If it appears, the installation is successful

Alternatively, test the libraries in OSGeo4W Shell:

```bash
python -c "import numpy scipy pandas geopandas shapely rasterio xarray matplotlib pyproj netCDF4 cftime; print('All libraries imported successfully!')"
```

# Contact info
Yingkui Li

Department of Geography & Sustainability

University of Tennessee

Knoxville, TN 37996

Email: yli32@utk.edu

Website: https://geography.utk.edu/about-us/faculty/dr-yingkui-li/

Google Scholar: https://scholar.google.com/citations?user=JoNuyCMAAAAJ&hl=en&oi=ao
