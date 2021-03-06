# Streamlit - Drawable Canvas

Streamlit component which provides a sketching canvas using [Fabric.js](http://fabricjs.com/).

![](./img/demo.gif)

## Installation

```shell script
pip install streamlit-drawable-canvas
```

## Example Usage

```python
import streamlit as st
from streamlit_drawable_canvas import st_canvas

# Specify brush parameters and drawing mode
stroke_width = st.sidebar.slider("Stroke width: ", 1, 100, 10)
stroke_color = st.sidebar.beta_color_picker("Stroke color hex: ")
bg_color = st.sidebar.beta_color_picker("Background color hex: ", "#eee")
bg_image = st.sidebar.file_uploader("Background image:", type=["png", "jpg"])
drawing_mode = st.sidebar.selectbox(
    "Drawing tool:", ("freedraw", "line", "rect", "transform")
)

# Create a canvas component
canvas_result = st_canvas(
    fill_color="rgba(255, 165, 0, 0.3)",  # Fixed fill color with some opacity
    stroke_width=stroke_width,
    stroke_color=stroke_color,
    background_color="" if bg_image else bg_color,
    background_image=Image.open(bg_image) if bg_image else None,
    height=150,
    drawing_mode=drawing_mode,
    key="canvas",
)

# Do something interesting with the image data
if canvas_result.image_data is not None:
    st.image(canvas_result.image_data)
    st.dataframe(pd.json_normalize(canvas_result.json_data["objects"]))
```

## Development

### Install

- JS side

```shell script
cd frontend
npm install
```

- Python side

```shell script
conda create -n streamlit-drawable-canvas python=3.7
conda activate streamlit-drawable-canvas
pip install -e .
```

### Run

Both webpack dev server and Streamlit should run at the same time.

- JS side

```shell script
cd frontend
npm run start
```

- Python side

```shell script
streamlit run app.py
```

## References

- [react-sketch](https://github.com/tbolis/react-sketch)
- [React hooks - fabric](https://github.com/fabricjs/fabric.js/issues/5951#issuecomment-563427231)
- [Simulate Retina display](https://stackoverflow.com/questions/12243549/how-to-test-a-webpage-meant-for-retina-display)
- [High DPI Canvas](https://www.html5rocks.com/en/tutorials/canvas/hidpi/)
- [Drawing with FabricJS and TypeScript Part 2: Straight Lines](https://exceptionnotfound.net/drawing-with-fabricjs-and-typescript-part-2-straight-lines/)
- [Types for classes as values in TypeScript](https://2ality.com/2020/04/classes-as-values-typescript.html)
