# file upload

```python,icon=.devicon-python-plain
import os

import docx2txt  # pip install docx2txt
import fitz  # pip install PyMuPDF
import pandas as pd  # pip install pandas
import streamlit as st
from PIL import Image  # pip install pillow
from streamlit.runtime.uploaded_file_manager import UploadedFile


def get_file_details(file: UploadedFile) -> dict[str, str | int]:
    return {"FileName": file.name, "FileType": file.type, "FileSize": file.size}


@st.cache_data
def load_image(img_file: UploadedFile) -> Image.Image:
    return Image.open(img_file)


def read_pdf(pdf_file: UploadedFile, page_number: int | None = None) -> list[str]:
    with fitz.open(stream=pdf_file.read(), filetype="pdf") as pdf_document:
        pages = len(pdf_document) if page_number is None else page_number
        return [pdf_document.load_page(p).get_text() for p in range(pages)]


def save_uploaded_file(uploaded_file, filename: str):
    path = os.path.join("./temp_dir", filename)
    with open(path, "wb") as f:
        f.write(uploaded_file.getbuffer())
    return st.success(f"Saved file in: {path}")


st.title("File Upload Tutorial")

menu = ["Home", "Dataset", "DocumentFiles", "Audio"]
choice = st.sidebar.selectbox("Menu", menu)

if choice == "Home":
    st.subheader("Home")
    image_files = st.file_uploader(
        "Upload Image", type=["png", "jpg", "jpeg"], accept_multiple_files=True
    )
    if image_files is not None:
        for image_file in image_files:
            st.write(get_file_details(image_file))
            st.image(load_image(image_file))
            save_uploaded_file(image_file, image_file.name)
elif choice == "Dataset":
    st.subheader("Dataset")
    data_file = st.file_uploader("Upload CSV", type=["csv"])
    if data_file is not None:
        st.write(get_file_details(data_file))
        df = pd.read_csv(data_file)
        st.dataframe(df)
        edited_df = st.data_editor(df)

        st.download_button(
            label="Download data as CSV",
            data=df.to_csv().encode("utf-8"),
            file_name="large_df.csv",
            mime="text/csv",
        )

        st.download_button(
            label="Download edit_data as CSV",
            data=edited_df.to_csv().encode("utf-8"),
            file_name="large_df.csv",
            mime="text/csv",
        )
elif choice == "DocumentFiles":
    st.subheader("DocumentFiles")
    doc_file = st.file_uploader("Upload Document", type=["pdf", "docx", "txt"])
    file_tpe = {
        "txt": "text/plain",
        "pdf": "application/pdf",
        "docx": "application/vnd.openxmlformats-officedocument.wordprocessingml.document",
    }
    if doc_file is not None:
        st.write(get_file_details(doc_file))
        if doc_file.type == file_tpe["txt"]:
            text = str(doc_file.read(), encoding="utf-8")
            st.text(text)  # 用 st.write(text) 換變成 markdown
        elif doc_file.type == file_tpe["pdf"]:
            texts = read_pdf(doc_file)
            for i, text in enumerate(texts):
                st.subheader(f"Page {i + 1}")
                st.text(text)
                st.divider()
        elif doc_file.type == file_tpe["docx"]:
            text = docx2txt.process(doc_file)
            st.text(text)
        else:
            st.warning("File type not supported")
elif choice == "Audio":
    st.subheader("Audio")
    audio_file = st.file_uploader("Upload Audio", type=["mp3", "wav", "m4a", "flac"])
    if audio_file is not None:
        st.write(get_file_details(audio_file))
        st.audio(audio_file)

        st.download_button("Download Audio", audio_file, "audio.mp3", "audio/mp3")
```
