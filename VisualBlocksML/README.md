# Visual Blocks for ML

[Visual Blocks for ML](https://visualblocks.withgoogle.com) is a new JavaScript framework from Google for rapid prototyping and experimentation for various ML tasks. You can connect ML Blocks in endless configurations to build highly interactive experiences in minutes. Off-the-shelf blocks include models, user inputs, processors, and visualizations.

### Read in the TFLite file
```
with open('autocomplete.tflite', 'rb') as file:
    model = file.read()
```


### Inference helper function

```
def run_inference(input):
  interp = interpreter.InterpreterWithCustomOps(
      model_content=model,
      custom_op_registerers=tf_text.tflite_registrar.SELECT_TFTEXT_OPS)
  interp.get_signature_list()

  generator = interp.get_signature_runner('serving_default')
  output = generator(prompt=np.array([input]))
  output_text = output["output_0"].item(0).decode('utf-8')
  return output_text
  ```

### Import Visual Blocks

```
!pip install visualblocks

import visualblocks
```

### Start Visual Blocks server and display UI


```
server = visualblocks.Server(text_to_text=run_inference)
```

```
server.display()
```

### Referances
Google i/o  -2023 [colab](https://colab.research.google.com/github/tensorflow/codelabs/blob/main/KerasNLP/io2023_workshop.ipynb#scrollTo=nsqVFGilThAS)