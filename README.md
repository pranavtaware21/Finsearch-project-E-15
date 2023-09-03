#Finsearch Project

import numpy as np
from scipy.stats import norm

def black_scholes(S, K, T, r, sigma, option_type='call'):
    """
    Calculate the Black-Scholes option price.

    S: Current stock price
    K: Strike price
    T: Time to expiration (in years)
    r: Risk-free interest rate (annual)
    sigma: Volatility (annual)
    option_type: 'call' for call option, 'put' for put option

    Returns the option price.
    """
    d1 = (np.log(S / K) + (r + (sigma**2) / 2) * T) / (sigma * np.sqrt(T))
    d2 = d1 - sigma * np.sqrt(T)

    if option_type == 'call':
        option_price = S * norm.cdf(d1) - K * np.exp(-r * T) * norm.cdf(d2)
    elif option_type == 'put':
        option_price = K * np.exp(-r * T) * norm.cdf(-d2) - S * norm.cdf(-d1)
    else:
        raise ValueError("Invalid option type. Use 'call' or 'put'.")

    return option_price

# Example usage
stock_price = 100  # Current stock price
strike_price = 100  # Strike price
time_to_expiry = 1  # Time to expiration in years
risk_free_rate = 0.05  # Annual risk-free interest rate
volatility = 0.2  # Annual volatility

call_option_price = black_scholes(stock_price, strike_price, time_to_expiry, risk_free_rate, volatility, option_type='call')
put_option_price = black_scholes(stock_price, strike_price, time_to_expiry, risk_free_rate, volatility, option_type='put')

print(f"Call Option Price: {call_option_price}")
print(f"Put Option Price: {put_option_price}") 
