# Option Greeks Analysis
This project implements the Black-Scholes model for pricing European options and calculating the Greeks: Delta, Gamma, Vega, Theta, and Rho. It also generates heatmaps for these values to visualize how they change with volatility and underlying price.

## Features
- Calculates option price using the Black-Scholes formula.
- Computes Greeks to measure option risk sensitivity.
- Generates heatmaps for option price and Greeks.
- User input for underlying price, strike price, time to expiration, risk-free rate, volatility, and option type (Call or Put).

## Dependencies
- Python 3.x
- NumPy
- SciPy
- Matplotlib
- Seaborn

## Installation
Ensure you have Python installed and install the required libraries:
```sh
pip install numpy scipy matplotlib seaborn
```

## Usage
Run the script and provide the required inputs when prompted:
```sh
python option_greeks_analysis.py
```

## Output
- Prints the Black-Scholes price and Greeks for the given inputs.
- Displays heatmaps for visual analysis.

## Example Input
```
Enter Underlying Price: 100
Enter Strike Price: 105
Date Till Expiration: 0.5
Risk-Free Rate: 0.05
Volatility: 0.2
Enter option type (C for Call, P for Put): C
```

## Example Output
```
Option is Call: $4.3295
Delta: 0.4602
Gamma: 0.0187
Vega: 0.3745
Theta: -0.0173
Rho: 2.2345
```

## License
This project is licensed under the MIT License.

