# ML-GB SC-CO2

Prediction of binary diffusivities in supercritical carbon dioxide

This tool estimates the binary diffusivity of a solute in supercritical carbon dioxide using a machine learning model trained with 4000 experimental data points from over 170 systems.

## Requirements

Python 3 and the following Python libraries are also required:
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

Call the program and provide the five properties as float in the following order:
1. Temperature (K)
2. Density (g/cm3)
3. Solute molecular mass (g/mol)
4. Solute critical pressure (bar)
5. Solute acentric factor (-)


```python
python ml_sc_co2 --properties YOUR_TEMPERATURE YOUR_DENSITY YOUR_MOLECULAR_MASS YOUR_CRITICAL_PRESSURE YOUR_ACENTRIC_FACTOR
```

Example:

```python
python ml_sc_co2 --properties 313.15 0.830000647 430.71 8.45543 0.8071

# Output:
# Predicted diffusivities:
# D12(1) = 5.81821846E-05 cm2/s
```


### Option 2) By specifying each property:

In this case the order is irrelevant. 

```python
python ml_sc_co2 --temperature YOUR_TEMPERATURE --density YOUR_DENSITY --molecularmass YOUR_MOLECULAR_MASS --criticalpressure YOUR_CRITICAL_PRESSURE --acentricfactor YOUR_ACENTRIC_FACTOR

# OR using 

python ml_sc_co2 -t YOUR_TEMPERATURE -d YOUR_DENSITY -mm YOUR_MOLECULAR_MASS -cp YOUR_CRITICAL_PRESSURE -af YOUR_ACENTRIC_FACTOR
```

Example:

```python
python ml_sc_co2 -t 313.15 -d 0.830000647 -mm 430.71 -cp 8.45543 -af 0.8071

# Output:
# Predicted diffusivities:
# D12(1) = 5.81821846E-05 cm2/s
```


### Option 3) By specifying a data CSV file with the input data:

The CSV file must include at least five columns with the following names: `T`, `density`, `solute.M2`, `solute.Pc`, and `solute.w`. You can provide any number of points as rows.

```python
python ml_sc_co2 --csvfile YOUR_CSVFILE_PATH
```

Example:

```python
# Using a file in the same directory with 3 points (rows)
python ml_sc_co2 --csvfile data.csv

# Output:
# Predicted diffusivities:
# D12(1) = 5.03732712E-05 cm2/s
# D12(2) = 1.05026748E-04 cm2/s
# D12(3) = 9.14913157E-05 cm2/s
```

### Save results

Optionally you can use the `--save` or `-s` flag to save the results in an csv file.

```python
python ml_sc_co2 --csvfile YOUR_CSVFILE_PATH --save
```


### Help 

```python
python ml_sc_co2 -h
```

```
usage: predict [-h]
               [-p TEMPERATURE DENSITY MOLECULAR_MASS CRITICAL_PRESSURE ACENTRIC_FACTOR]
               [-t TEMPERATURE] [-d DENSITY] [-mm MOLECULARMASS]
               [-cp CRITICALPRESSURE] [-af ACENTRICFACTOR] [-f CSVFILE] [-s]

Supercritical carbon dioxide diffusivity estimator

optional arguments:
  -h, --help            show this help message and exit
  -p TEMPERATURE DENSITY MOLECULAR_MASS CRITICAL_PRESSURE ACENTRIC_FACTOR, --properties TEMPERATURE DENSITY MOLECULAR_MASS CRITICAL_PRESSURE ACENTRIC_FACTOR
                        Temperature (K), Density (g/cm3), Solute molecular
                        mass (g/mol), Solute critical pressure (bar), Solute
                        acentric factor. Provided in this order.
  -t TEMPERATURE, --temperature TEMPERATURE
                        Temperature in K
  -d DENSITY, --density DENSITY
                        Density in g/cm3
  -mm MOLECULARMASS, --molecularmass MOLECULARMASS
                        Solute molecular mass in g/mol
  -cp CRITICALPRESSURE, --criticalpressure CRITICALPRESSURE
                        Solute critical pressure in bar
  -af ACENTRICFACTOR, --acentricfactor ACENTRICFACTOR
                        Solute acentric factor
  -f CSVFILE, --csvfile CSVFILE
                        Path to CSV file with input data
  -s, --save            Save results to file
```


