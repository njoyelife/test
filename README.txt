import matplotlib.pyplot as plt
import streamlit as st
import pandas as pd
import altair as alt
import numpy as np

from urllib.error import URLError

st.title("^GSPC")
st.write("""# THIS WORKED""")

input1 = input('Enter .csv file name with extension .csv below:')

print(input1)

ticker = input1

df = pd.read_csv(ticker)

df['Date'] = pd.to_datetime(df['Date'])
df['Open'] = pd.to_numeric(df['Open'])
df['High'] = pd.to_numeric(df['High'])
df['Low'] = pd.to_numeric(df['Low'])
df['Close*'] = pd.to_numeric(df['Close*'])
df['Adj Close**'] = pd.to_numeric(df['Adj Close**'])
df['Volume'] = pd.to_numeric(df['Volume']) #need to fix the - in volume

fig, ax = plt.subplots()

fig.set_figheight(5)
fig.set_figwidth(16.5)
fig.autofmt_xdate()
fig.tight_layout()

x = df['Date']
y = df['Close*']

ax.plot(x, y, color='r', lw=2, label='S&P500')
ax.set_yscale('log')
ax.set_title('Market Direction')
ax.set_xlabel('Date')
ax.set_ylabel('Price (USD)')
ax.legend(loc='upper left')

st.pyplot(fig)
