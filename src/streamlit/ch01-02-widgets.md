# Data elements

```python,icon=.devicon-python-plain
import streamlit as st
import pandas as pd

df = pd.DataFrame({
    'first column': [1, 2, 3, 4],
    'second column': [10, 20, 30, 40],
})

st.dataframe(df)  # st.write(df)
st.dataframe(df, width=200, height=100)
st.dataframe(df.style.highlight_max(axis=0))
st.table(df)

st.json({"data": "name"})  # st.write({"data": "name"})
```
