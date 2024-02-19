# Text elements

```python,icon=.devicon-python-plain
import streamlit as st

st.text("Hello, world!")
st.header("This is a header")
st.subheader("This is a subheader")
st.title("This is a title")
st.markdown("This is a markdown")
st.caption("This is a :blue[caption]. :rainbow[This is a rainbow]")
st.write(":colors[blue, green, orange, red, violet, gray/grey, rainbow.]")

st.code("print('Hello, world!')")
code_str = """
def hello(name: str) -> None:
    print(f"Hello, {name}!")
"""
st.code(code_str, language="python")

st.success("This is a success")
st.warning("This is a warning")
st.info("This is an info")
st.error("This is an error")
st.exception("This is an exception")

st.write("This is a write")
st.write('Hello, *World!* :sunglasses:')
st.write(1 + 1)
st.write([1, 2, 3])

st.help(range)  # st.write(range)
```
