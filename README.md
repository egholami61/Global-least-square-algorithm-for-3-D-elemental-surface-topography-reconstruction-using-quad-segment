### README Guide for Using Simulation Data in Micro-PIXE Analysis Code

This guide provides instructions for preparing and replacing the necessary data files in the Python script for the Micro-PIXE (Particle-Induced X-ray Emission) analysis. The script requires specific datasets such as range data, energy data, cross-section data, and stopping power data to accurately compute the elemental mapping of the sample.

#### 1. Preparing Your Data Files

You will need the following data sets to replace the placeholders in the Python script:

1. **Range Data (`R`)**: The range of ion energies in microns.
2. **Energy Data (`E`)**: The energy levels of the ions in MeV or other relevant units.
3. **Cross-Section Data (`Cr`)**: The X-ray production cross-section data corresponding to the energy levels.
4. **Stopping Power Data (`Sp` or `Es`)**: The stopping power of the material for ions at different energy levels.

#### 2. Data Format and File Structure

Your data files should be formatted as Excel files (`.xls`) or any compatible format that can be read using `pandas` or `numpy` libraries in Python. The script reads data from specific ranges within an Excel sheet. Ensure that the data is organized correctly in the specified sheet and range.

**Example Excel File Structure**: 
The Excel file should contain columns like the following:

| Column | Description                                     | Cell Range      |
|--------|-------------------------------------------------|-----------------|
| H      | Range data (`R`) in microns                     | `H2:H61`        |
| J      | Initial energy data (`E0`) in MeV               | `J2:J61`        |
| C      | Energy data (`E`) in MeV                        | `C3:C62`        |
| E      | Cross-section data (`Cr`) in barns              | `E3:E62`        |
| J      | Stopping power data (`Es`) in MeV/(mg/cm²)      | `J2:J61`        |
| L      | Stopping power data (`Sp`) in MeV/(mg/cm²)      | `L2:L61`        |

Make sure your file follows this structure and the data is correctly placed in the specified cell ranges.

#### 3. Replacing Placeholder Data in the Python Script

Update the following lines in your Python script to load your actual data from the Excel file:


# Load the data from your file
file_path = 'D:\\Proposal\\RADIATE\\MIC\\TNA 1\\Shell4\\Ca\\G2S_GLS\\Book1.xls'  # Replace with your file path

# Reading data from Excel file
R = pd.read_excel(file_path, sheet_name=1, usecols="H", skiprows=1, nrows=60).values.flatten()  # Range data
E0 = pd.read_excel(file_path, sheet_name=1, usecols="J", skiprows=1, nrows=60).values.flatten()  # Initial energy data
E = pd.read_excel(file_path, sheet_name=1, usecols="C", skiprows=2, nrows=60).values.flatten()  # Energy data
Cr = pd.read_excel(file_path, sheet_name=1, usecols="E", skiprows=2, nrows=60).values.flatten()  # Cross-section data
Es = pd.read_excel(file_path, sheet_name=1, usecols="J", skiprows=1, nrows=60).values.flatten()  # Stopping power data
Sp = pd.read_excel(file_path, sheet_name=1, usecols="L", skiprows=1, nrows=60).values.flatten()  # Stopping power data
```

#### 4. Defining Material Constants

Replace the following constants with values appropriate for your specific material:

Con = 0.20 * 4.856  # Concentration of Ca in CaCO3 (atoms/cm³ * 10^24)
mu = 1 / 50.1324  # Attenuation length for Cu-Ka radiation in microns, replace with the correct value for your material
```

You should adjust `Con` and `mu` based on the elemental concentration and the attenuation coefficient relevant to your sample.

#### 5. Running the Code

Once you have replaced the placeholders with your data:

1. Save the main script.
2. Run the script in your MATLAB environment.

#### 6. Visualizing the Results

The script generates several plots to visualize the reconstructed surface topography and X-ray yields:

- **Gradient Components (`Gx` and `Gy`)**: Gradient maps of the surface.
- **Topography Reconstruction**: Reconstructed 3-D topography of the sample.
  
Adjust plot settings as needed to customize the visualization according to your analysis requirements.

#### 7. Additional Notes

- **File Paths**: Ensure all file paths are correct and accessible. Use double backslashes (`\\`) in file paths for Windows compatibility.
- **Data Validity**: Verify that your data is accurate and in the correct units.


#### 8. Troubleshooting

- **File Not Found Error**: Ensure that the file paths are correct.
- **Data Range Errors**: Make sure the data in your Excel files match the specified ranges.
- **Syntax Errors**: Check for any missing or extra characters in the MATLAB script.

By following these guidelines, you will be able to replace the placeholders in the script with your actual data, ensuring accurate simulation and analysis results.
