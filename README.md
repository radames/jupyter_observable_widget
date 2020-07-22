# UMAP + Jupyter Notebook + ScatterGL 

Orignal notebook here https://observablehq.com/@radames/umap-jupyter-notebook-scattergl

Inspired by [Thomas](https://observablehq.com/@ballingt) notebook [visualize-a-data-frame-with-observable-in-jupyter](https://observablehq.com/@observablehq/visualize-a-data-frame-with-observable-in-jupyter)

Could the dataframe be re-rendered inside jupyter and have observable updated the visualization?

You can read a discussion on the topic [Observable Forum](https://talk.observablehq.com/t/jupyter-observable/2912)

Here is the [Jupyter notebook source code and preview](https://colab.research.google.com/drive/1KGhHdfbCzmlt4HTGPy7P9XOa1EloPkmf#scrollTo=1BfZota4SLpH) on google collab. Please change parameters and re-run cells to see it in action.

![](https://static.observableusercontent.com/files/ed5cfb60c553495d60d2dabd62e1c40075ba1648dcadf237d67eb36e4ac3d1afa6cc600ee5690b4c96d50d7d743b4c481c4002cf6afee34e6d79ae0e73ff9473)

### How it works

This Observable notebook is used as a reference vizualization. Using ScatterGL to plot 2D/3D points as a scatter plot.

You have to pass an array of 2D or 3D points to the HTML embed code. Then use Observable runtime to redefine the variables from your jupyter notebook.

Here is the jupyter python code with redifines. The data is serialize and dumped as string into the embed code.😛    

```python
def make_viz_embed(data, colors = [], labels = []):
  embed = f"""
    <div id="observablehq-0842ed87"></div>
    <script type="module">
    import {{Runtime, Inspector }} from "https://cdn.jsdelivr.net/npm/@observablehq/runtime@4/dist/runtime.js";
    import define from "https://api.observablehq.com/d/8bcaee9a68db388d.js?v=3";
    const inspect = Inspector.into("#observablehq-0842ed87");
    const notebook = (new Runtime).module(define, name => (name === "containerEl") && inspect());
    notebook.redefine('points', {json.dumps(data)})
    notebook.redefine('colors', {json.dumps(colors)})
    notebook.redefine('labels', {json.dumps(labels)})
    </script>
  """
  return embed
```
