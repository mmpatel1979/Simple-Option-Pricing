import numpy as np
import matplotlib.pyplot as plt
from scipy.stats import norm
import seaborn as sns

# Variable Inputs
S = float(input("Enter Underlying Price: "))                                    # Underlying Price
K = float(input("Enter Strike Price: "))                                        # Strike Price
T = float(input("Date Till Expiration: "))                                      # DTE
r = float(input("Risk-Free Rate: "))                                            # Risk-Free Rate
v = float(input("Volatility: "))                                                # Volatility (σ)
type = input("Enter option type (C for Call, P for Put): ").strip().upper()     # Contract Type

# Metric Calculations
d1 = (np.log(S/K) + (r + 0.5 * v ** 2)*T)/(v * np.sqrt(T))
d2 = d1 - v * np.sqrt(T)

# Black Scholes Calculations
def black_scholes(r, v, T, K, S, type):
    d1 = (np.log(S / K) + (r + 0.5 * v ** 2) * T) / (v * np.sqrt(T))
    d2 = d1 - v * np.sqrt(T)
    try:
        if type == "C":
            black_scholes = (S * norm.cdf(d1, 0, 1)) - (K * np.exp(-r * T) * norm.cdf(d2, 0, 1))
        elif type == 'P':
            black_scholes = (K * np.exp(-r * T) * norm.cdf(-d2, 0, 1)) - (S * norm.cdf(-d1, 0, 1))
        return black_scholes
    except:
        print("0")

# Delta Calculation
def delta(r, v, T, K, S, type):
    d1 = (np.log(S / K) + (r + 0.5 * v ** 2) * T) / (v * np.sqrt(T))
    try:
        if type == 'C':
            delta = norm.cdf(d1, 0, 1)
        elif type == 'P':
            delta = -norm.cdf(-d1, 0, 1)
        return delta
    except:
        print("0")

# Gamma Calculation
def gamma(r, v, T, K, S, type):
    d1 = (np.log(S / K) + (r + 0.5 * v ** 2) * T) / (v * np.sqrt(T))
    try:
        gamma = norm.pdf(d1, 0, 1) / (S * v * np.sqrt(T))
        return gamma
    except:
        print("0")

# Vega Calculation
def vega(r, v, T, K, S, type):
    d1 = (np.log(S / K) + (r + 0.5 * v ** 2) * T) / (v * np.sqrt(T))
    try:
        vega = S * norm.pdf(d1, 0, 1) * np.sqrt(T)
        return vega * 0.01
    except:
        print("0")

# Theta Calculation
def theta(r, v, T, K, S, type):
    d1 = (np.log(S / K) + (r + 0.5 * v ** 2) * T) / (v * np.sqrt(T))
    d2 = d1 - v * np.sqrt(T)
    try:
        if type == 'C':
            theta = (-S * norm.pdf(d1, 0, 1) * v/(2 * np.sqrt(T))) - (r * K * np.exp(-r * T) * norm.cdf(d2, 0, 1))
        elif type == 'P':
            theta = (-S * norm.pdf(d1, 0, 1) * v/(2 * np.sqrt(T))) + (r * K * np.exp(-r * T) * norm.cdf(-d2, 0, 1))
        return theta / 365
    except:
        print("0")

# Rho Calculation
def rho(r, v, T, K, S, type):
    d1 = (np.log(S / K) + (r + 0.5 * v ** 2) * T) / (v * np.sqrt(T))
    d2 = d1 - v * np.sqrt(T)
    try:
        if type == 'C':
            rho = K * T * np.exp(-r * T) * norm.cdf(d2, 0, 1)
        elif type == 'P':
            rho = -K * T * np.exp(-r * T) * norm.cdf(-d2, 0, 1)
        return rho * 0.01
    except:
        print("0")

# Heatmap Calculations
underlying = np.linspace(K - 25, K + 25, 10)
volatility = np.linspace(0.1, 1, 10)
greeks = {"Option Price": np.array([[black_scholes(r, v, T, K, S, type) for S in underlying] for v in volatility]),
          "Delta Price": np.array([[delta(r, v, T, K, S, type) for S in underlying] for v in volatility]),
          "Gamma Price": np.array([[gamma(r, v, T, K, S, type) for S in underlying] for v in volatility]),
          "Vega Price": np .array([[vega(r, v, T, K, S, type) for S in underlying] for v in volatility]),
          "Theta Price": np.array([[theta(r, v, T, K, S, type) for S in underlying] for v in volatility]),
          "Rho Price": np.array([[rho(r, v, T, K, S, type) for S in underlying] for v in volatility]),
         }

# Creating Heatmap
cmap_dict = {"Option Price": "Greys",
             "Delta Price": "Blues",
             "Gamma Price": "Greens",
             "Vega Price": "RdPu",
             "Theta Price": "Purples",
             "Rho Price": "Reds"
            }

for greek, data in greeks.items():
    plt.figure(figsize=(12, 6))
    sns.heatmap(data, xticklabels=np.round(underlying, 2), yticklabels=np.round(volatility * 100, 1), cmap=cmap_dict[greek], annot=True, fmt=".2f")
    plt.xlabel("Underlying Price")
    plt.ylabel("Volatility (%)")
    plt.title(f"{greek} Heatmap")
    plt.show()

# Printing Metrics
print(f'Option is { "Call" if type == "C" else "Put" }: $', round(black_scholes(r, v, T, K, S, type), 4))
print('Delta is: $', round(delta(r, v, T, K, S, type), 4))
print('Gamma is: $', round(gamma(r, v, T, K, S, type), 4))
print('Vega is: $', round(vega(r, v, T, K, S, type), 4))
print('Theta is: $', round(theta(r, v, T, K, S, type), 4))
print('Rho is: $', round(rho(r, v, T, K, S, type), 4))
