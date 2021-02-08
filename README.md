# Machine Learning models for D12 prediction

Prediction of binary diffusivities of solutes in:
- supercritical carbon dioxide
- polar solvents (except water) 
- nonpolar solvents (except supercritical carbon dioxide)

The machine learning models were trained with a database of 4000 experimental data points from over 170 systems. For more information check the following papers:

- [J.P.S. Aniceto, B. Zêzere, C.M. Silva. Machine learning models for the prediction of diffusivities in supercritical CO2 systems, Journal of Molecular Liquids (2021) 115281.](https://www.sciencedirect.com/science/article/pii/S0167732221000076)
- [J.P.S. Aniceto, B. Zêzere, C.M. Silva. Predictive Models for the Binary Diffusion Coefficient at Infinite Dilution in Polar and Nonpolar Fluids, Materials 14 (2021) 542.](https://www.mdpi.com/1996-1944/14/3/542)

## Index
  * [Quickstart](#quickstart)
  * [Requirements](#requirements)
  * [Installation](#installation)
  * [Usage](#usage)
    + [Option 1) By providing the properties in order:](#option-1--by-providing-the-properties-in-order-)
    + [Option 2) By specifying each property:](#option-2--by-specifying-each-property-)
    + [Option 3) By specifying a CSV file with the input data:](#option-3--by-specifying-a-csv-file-with-the-input-data-)
    + [Save results](#save-results)
    + [Help](#help)
  * [Citing](#citing)


## Quickstart

Select the program and provide the properties using their flags. 

| Solvent | Program | Required properties (unit) [-flag] |
|-|-|-|
| SC-CO2 | ml_scco2.py | Temperature (K) [-t]<br>Density (g/cm3) [-d]<br>Solute Molar Mass (g/mol) [-mm]<br>Solute Critical Pressure (bar) [-cp]<br>Solute Acentric Factor (-) [-af] |
| Polar | ml_polar.py | Temperature (K) [-t]<br>Viscosity (cP) [-v]<br>Solute Molar Mass (g/mol) [-m2]<br>Solute Critical Pressure (bar) [-cp2]<br>Solvent Molar Mass (g/mol) [-m1]<br>Solvent Lennard-Jones Energy (K) -[e1] |
| Nonpolar | ml_nonpolar.py | Temperature (K) [-t]<br>Viscosity (cP) [-v]<br>Solute Molar Mass (g/mol) [-m2]<br>Solute Critical Pressure (bar) [-cp2]<br>Solvent Molar Mass (g/mol) [-m1] |

Example:

```python
python ml_scco2.py -t 313.15 -d 0.830000647 -mm 430.71 -cp 8.45543 -af 0.8071

# Output:
# Predicted diffusivities:
# D12(1) = 5.81821846E-05 cm2/s
```

You can also calculate multiple points by providing the properties as a CSV file. See below.


## Requirements

Python 3 and the following Python libraries are required:
- numpy
- pandas
- scikit-learn
- joblib

Program is fully tested on:
- Python 3.7
- numpy 1.18.5
- pandas 1.0.5
- scikit-learn 0.23.1 

## Installation

1. Install Python from [python.org](https://www.python.org/).
2. Download the software by clickig `Code` >> `Download ZIP`. 
3. Unpack the zip file.
4. Open the command line and run `pip install -r requirements.txt` to install the required libraries.
5. You can now `cd` to the program folder and use it as described below.


## Usage

### Option 1) By providing the properties in order:

Call the program you desire and provide the properties in order. For istance, for the SC-CO2 program:
1. Temperature (K)
2. Density (g/cm3)
3. Solute molecular mass (g/mol)
4. Solute critical pressure (bar)
5. Solute acentric factor (-)


```python
python ml_scco2.py --properties YOUR_TEMPERATURE YOUR_DENSITY YOUR_MOLECULAR_MASS YOUR_CRITICAL_PRESSURE YOUR_ACENTRIC_FACTOR
```

Example:

```python
python ml_scco2.py --properties 313.15 0.830000647 430.71 8.45543 0.8071

# Output:
# Predicted diffusivities:
# D12(1) = 5.81821846E-05 cm2/s
```


### Option 2) By specifying each property:

In this case the order is irrelevant. 

```python
python ml_scco2.py --temperature YOUR_TEMPERATURE --density YOUR_DENSITY --molecularmass YOUR_MOLECULAR_MASS --criticalpressure YOUR_CRITICAL_PRESSURE --acentricfactor YOUR_ACENTRIC_FACTOR

# OR using 

python ml_scco2.py -t YOUR_TEMPERATURE -d YOUR_DENSITY -mm YOUR_MOLECULAR_MASS -cp YOUR_CRITICAL_PRESSURE -af YOUR_ACENTRIC_FACTOR
```

Example:

```python
python ml_scco2.py -t 313.15 -d 0.830000647 -mm 430.71 -cp 8.45543 -af 0.8071

# Output:
# Predicted diffusivities:
# D12(1) = 5.81821846E-05 cm2/s
```


### Option 3) By specifying a CSV file with the input data:

The CSV file must include at least five columns with the following headers: 

| Case | SC-CO2 | Polar | Nonpolar |
|-|-|-|-|
| Properties/Headers | T<br>density<br>solute.M2<br>solute.Pc<br>solute.w | T<br>viscosity<br>solute.M2<br>solute.Pc<br>solvent.M1<br>solvent.elj | T<br>viscosity<br>solute.M2<br>solute.Pc<br>solvent.M1 |

You can provide any number of points as rows. See the `examples` folder.

```python
python ml_scco2.py --csvfile YOUR_CSVFILE_PATH
```

Example:

```python
# Using a file in the same directory with 3 points (rows)
python ml_scco2.py --csvfile sample-scco2-data.csv

# Output:
# Predicted diffusivities:
# D12(1) = 5.03732712E-05 cm2/s
# D12(2) = 1.05026748E-04 cm2/s
# D12(3) = 9.14913157E-05 cm2/s
```

### Save results

Optionally you can use the `--save` or `-s` flag to save the results in an csv file.

```python
python ml_scco2.py --csvfile YOUR_CSVFILE_PATH --save
```


### Help 

```python
python ml_scco2.py -h
```


## Citing

If you use the SC-CO2 model/program for a scientific publication, please cite:

- [J.P.S. Aniceto, B. Zêzere, C.M. Silva. Machine learning models for the prediction of diffusivities in supercritical CO2 systems, Journal of Molecular Liquids (2021) 115281.](https://www.sciencedirect.com/science/article/pii/S0167732221000076)

If you use the polar or nonpolar models/programs for a scientific publication, please cite:
- [J.P.S. Aniceto, B. Zêzere, C.M. Silva. Predictive Models for the Binary Diffusion Coefficient at Infinite Dilution in Polar and Nonpolar Fluids, Materials 14 (2021) 542.](https://www.mdpi.com/1996-1944/14/3/542)
