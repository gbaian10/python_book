# form

```python,icon=.devicon-python-plain
from time import sleep

import streamlit as st

with st.form(key="my_form", clear_on_submit=True):
    col1, col2, col3 = st.columns([3, 1, 2])
    with col1:
        amount = st.number_input("Enter the amount", value=50)
    with col2:
        hours_per_week = st.number_input("Enter the hours", 1, 120)
    with col3:
        st.text("Salary")
        submit_button = st.form_submit_button(label="Calculate")

if submit_button:
    with st.expander("Results", expanded=True):
        with st.spinner("Calculating..."):
            sleep(1.5)
            st.write(f"Your salary is: {amount * hours_per_week}")
```