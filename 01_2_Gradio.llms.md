# Gradio

Gradio

Author

Benedict Thekkel

``` python
!pip list | grep gradio
```

    gradio                              4.27.0
    gradio_client                       0.15.1

## Basic Interface: text, slider -\> text

``` python
import gradio as gr

def greet(name, intensity):
    return "Hello, " + name + "!" * int(intensity)

demo = gr.Interface(
    fn=greet,
    inputs=["text", "slider"],
    outputs=["text"],
)

demo.launch()
```

    Running on local URL:  http://127.0.0.1:7860

    To create a public link, set `share=True` in `launch()`.

``` python
gr.Interface(
    fn: 'Callable',
    inputs: 'str | Component | list[str | Component] | None',
    outputs: 'str | Component | list[str | Component] | None',
    examples: 'list[Any] | list[list[Any]] | str | None' = None,
    cache_examples: "bool | Literal['lazy'] | None" = None,
    examples_per_page: 'int' = 10,
    live: 'bool' = False,
    title: 'str | None' = None,
    description: 'str | None' = None,
    article: 'str | None' = None,
    thumbnail: 'str | None' = None,
    theme: 'Theme | str | None' = None,
    css: 'str | None' = None,
    allow_flagging: "Literal['never'] | Literal['auto'] | Literal['manual'] | None" = None,
    flagging_options: 'list[str] | list[tuple[str, str]] | None' = None,
    flagging_dir: 'str' = 'flagged',
    flagging_callback: 'FlaggingCallback | None' = None,
    analytics_enabled: 'bool | None' = None,
    batch: 'bool' = False,
    max_batch_size: 'int' = 4,
    api_name: 'str | Literal[False] | None' = 'predict',
    _api_mode: 'bool' = False,
    allow_duplication: 'bool' = False,
    concurrency_limit: "int | None | Literal['default']" = 'default',
    js: 'str | None' = None,
    head: 'str | None' = None,
    additional_inputs: 'str | Component | list[str | Component] | None' = None,
    additional_inputs_accordion: 'str | Accordion | None' = None,
    *,
    submit_btn: 'str | Button' = 'Submit',
    stop_btn: 'str | Button' = 'Stop',
    clear_btn: 'str | Button' = 'Clear',
    delete_cache: 'tuple[int, int] | None' = None,
    **kwargs,
)
```

## Image output: slider -\> image

``` python
import gradio as gr
import numpy as np
import time

def fake_diffusion(steps):
    rng = np.random.default_rng()
    for i in range(steps):
        time.sleep(1)
        image = rng.random(size=(600, 600, 3))
        yield image
    image = np.ones((1000,1000,3), np.uint8)
    image[:] = [255, 124, 0]
    yield image


demo = gr.Interface(fake_diffusion,
                    inputs=gr.Slider(1, 10, 3, step=1),
                    outputs="image")

demo.launch()
```

    Running on local URL:  http://127.0.0.1:7861

    To create a public link, set `share=True` in `launch()`.

## Progress bar: text -\> text

``` python
import gradio as gr
import time

def slowly_reverse(word, progress=gr.Progress()):
    progress(0, desc="Starting")
    time.sleep(1)
    progress(0.05)
    new_string = ""
    for letter in progress.tqdm(word, desc="Reversing"):
        time.sleep(0.25)
        new_string = letter + new_string
    return new_string

demo = gr.Interface(slowly_reverse, gr.Text(), gr.Text())

demo.launch()
```

    Running on local URL:  http://127.0.0.1:7862

    To create a public link, set `share=True` in `launch()`.

``` python
import gradio as gr

secret_word = "gradio"

with gr.Blocks() as demo:    
    used_letters_var = gr.State([])
    with gr.Row() as row:
        with gr.Column():
            input_letter = gr.Textbox(label="Enter letter")
            btn = gr.Button("Guess Letter")
        with gr.Column():
            hangman = gr.Textbox(
                label="Hangman",
                value="_"*len(secret_word)
            )
            used_letters_box = gr.Textbox(label="Used Letters")

    def guess_letter(letter, used_letters):
        used_letters.append(letter)
        answer = "".join([
            (letter if letter in used_letters else "_")
            for letter in secret_word
        ])
        return {
            used_letters_var: used_letters,
            used_letters_box: ", ".join(used_letters),
            hangman: answer
        }
    btn.click(
        guess_letter, 
        [input_letter, used_letters_var],
        [used_letters_var, used_letters_box, hangman]
        )
demo.launch()
```

    Running on local URL:  http://127.0.0.1:7863

    To create a public link, set `share=True` in `launch()`.

## Audio: audio -\> audio

``` python
import gradio as gr
from pydub import AudioSegment
from time import sleep

with gr.Blocks() as demo:
    input_audio = gr.Audio(label="Input Audio", type="filepath", format="mp3")
    with gr.Row():
        with gr.Column():
            stream_as_file_btn = gr.Button("Stream as File")
            format = gr.Radio(["wav", "mp3"], value="wav", label="Format")
            stream_as_file_output = gr.Audio(streaming=True)

            def stream_file(audio_file, format):
                audio = AudioSegment.from_file(audio_file)
                i = 0
                chunk_size = 1000
                while chunk_size * i < len(audio):
                    chunk = audio[chunk_size * i : chunk_size * (i + 1)]
                    i += 1
                    if chunk:
                        file = f"/tmp/{i}.{format}"
                        chunk.export(file, format=format)
                        yield file
                        sleep(0.5)

            stream_as_file_btn.click(
                stream_file, [input_audio, format], stream_as_file_output
            )

            gr.Examples(
                [["audio/cantina.wav", "wav"], ["audio/cantina.wav", "mp3"]],
                [input_audio, format],
                fn=stream_file,
                outputs=stream_as_file_output,
            )

        with gr.Column():
            stream_as_bytes_btn = gr.Button("Stream as Bytes")
            stream_as_bytes_output = gr.Audio(format="bytes", streaming=True)

            def stream_bytes(audio_file):
                chunk_size = 20_000
                with open(audio_file, "rb") as f:
                    while True:
                        chunk = f.read(chunk_size)
                        if chunk:
                            yield chunk
                            sleep(1)
                        else:
                            break
            stream_as_bytes_btn.click(stream_bytes, input_audio, stream_as_bytes_output)

if __name__ == "__main__":
    demo.queue().launch()
```

    Running on local URL:  http://127.0.0.1:7865

    To create a public link, set `share=True` in `launch()`.

    Traceback (most recent call last):
      File "/home/ben/mambaforge/envs/cfast/lib/python3.11/site-packages/gradio/queueing.py", line 527, in process_events
        response = await route_utils.call_process_api(
                   ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
      File "/home/ben/mambaforge/envs/cfast/lib/python3.11/site-packages/gradio/route_utils.py", line 261, in call_process_api
        output = await app.get_blocks().process_api(
                 ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
      File "/home/ben/mambaforge/envs/cfast/lib/python3.11/site-packages/gradio/blocks.py", line 1784, in process_api
        inputs = await self.preprocess_data(
                 ^^^^^^^^^^^^^^^^^^^^^^^^^^^
      File "/home/ben/mambaforge/envs/cfast/lib/python3.11/site-packages/gradio/blocks.py", line 1506, in preprocess_data
        processed_input.append(block.preprocess(inputs_cached))
                               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
      File "/home/ben/mambaforge/envs/cfast/lib/python3.11/site-packages/gradio/components/audio.py", line 231, in preprocess
        processing_utils.audio_to_file(
      File "/home/ben/mambaforge/envs/cfast/lib/python3.11/site-packages/gradio/processing_utils.py", line 560, in audio_to_file
        file = audio.export(filename, format=format)
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
      File "/home/ben/mambaforge/envs/cfast/lib/python3.11/site-packages/pydub/audio_segment.py", line 970, in export
        raise CouldntEncodeError(
    pydub.exceptions.CouldntEncodeError: Encoding failed. ffmpeg/avlib returned error code: 127

    Command:['ffmpeg', '-y', '-f', 'wav', '-i', '/tmp/tmplaiefr8j', '-f', 'mp3', '/tmp/tmpiojnrpsx']

    Output from ffmpeg/avlib:

    ffmpeg: error while loading shared libraries: libopenh264.so.5: cannot open shared object file: No such file or directory

    Traceback (most recent call last):
      File "/home/ben/mambaforge/envs/cfast/lib/python3.11/site-packages/gradio/queueing.py", line 527, in process_events
        response = await route_utils.call_process_api(
                   ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
      File "/home/ben/mambaforge/envs/cfast/lib/python3.11/site-packages/gradio/route_utils.py", line 261, in call_process_api
        output = await app.get_blocks().process_api(
                 ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
      File "/home/ben/mambaforge/envs/cfast/lib/python3.11/site-packages/gradio/blocks.py", line 1784, in process_api
        inputs = await self.preprocess_data(
                 ^^^^^^^^^^^^^^^^^^^^^^^^^^^
      File "/home/ben/mambaforge/envs/cfast/lib/python3.11/site-packages/gradio/blocks.py", line 1506, in preprocess_data
        processed_input.append(block.preprocess(inputs_cached))
                               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
      File "/home/ben/mambaforge/envs/cfast/lib/python3.11/site-packages/gradio/components/audio.py", line 231, in preprocess
        processing_utils.audio_to_file(
      File "/home/ben/mambaforge/envs/cfast/lib/python3.11/site-packages/gradio/processing_utils.py", line 560, in audio_to_file
        file = audio.export(filename, format=format)
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
      File "/home/ben/mambaforge/envs/cfast/lib/python3.11/site-packages/pydub/audio_segment.py", line 970, in export
        raise CouldntEncodeError(
    pydub.exceptions.CouldntEncodeError: Encoding failed. ffmpeg/avlib returned error code: 127

    Command:['ffmpeg', '-y', '-f', 'wav', '-i', '/tmp/tmpuqq4b20d', '-f', 'mp3', '/tmp/tmphx041ptn']

    Output from ffmpeg/avlib:

    ffmpeg: error while loading shared libraries: libopenh264.so.5: cannot open shared object file: No such file or directory

``` python
import torch

model = torch.hub.load('pytorch/vision:v0.6.0', 'resnet18', pretrained=True).eval()
```

    Downloading: "https://github.com/pytorch/vision/zipball/v0.6.0" to /home/ben/.cache/torch/hub/v0.6.0.zip
    /home/ben/mambaforge/envs/cfast/lib/python3.11/site-packages/torchvision/models/_utils.py:208: UserWarning: The parameter 'pretrained' is deprecated since 0.13 and may be removed in the future, please use 'weights' instead.
      warnings.warn(
    /home/ben/mambaforge/envs/cfast/lib/python3.11/site-packages/torchvision/models/_utils.py:223: UserWarning: Arguments other than a weight enum or `None` for 'weights' are deprecated since 0.13 and may be removed in the future. The current behavior is equivalent to passing `weights=ResNet18_Weights.IMAGENET1K_V1`. You can also use `weights=ResNet18_Weights.DEFAULT` to get the most up-to-date weights.
      warnings.warn(msg)

``` python
import requests
from PIL import Image
from torchvision import transforms

# Download human-readable labels for ImageNet.
response = requests.get("https://git.io/JJkYN")
labels = response.text.split("\n")

def predict(inp):
  inp = transforms.ToTensor()(inp).unsqueeze(0)
  with torch.no_grad():
    prediction = torch.nn.functional.softmax(model(inp)[0], dim=0)
    confidences = {labels[i]: float(prediction[i]) for i in range(1000)}
  return confidences
```

``` python
import gradio as gr

gr.Interface(fn=predict,
             inputs=gr.Image(type="pil"),
             outputs=gr.Label(num_top_classes=3),
             examples=["tiger.jpg", "cheetah.jpg"]).launch()
```

    Running on local URL:  http://127.0.0.1:7869

    Thanks for being a Gradio user! If you have questions or feedback, please join our Discord server and chat with us: https://discord.gg/feTf9x3ZSB

    To create a public link, set `share=True` in `launch()`.

    Traceback (most recent call last):
      File "/home/ben/mambaforge/envs/cfast/lib/python3.11/site-packages/gradio/queueing.py", line 527, in process_events
        response = await route_utils.call_process_api(
                   ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
      File "/home/ben/mambaforge/envs/cfast/lib/python3.11/site-packages/gradio/route_utils.py", line 261, in call_process_api
        output = await app.get_blocks().process_api(
                 ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
      File "/home/ben/mambaforge/envs/cfast/lib/python3.11/site-packages/gradio/blocks.py", line 1788, in process_api
        result = await self.call_function(
                 ^^^^^^^^^^^^^^^^^^^^^^^^^
      File "/home/ben/mambaforge/envs/cfast/lib/python3.11/site-packages/gradio/blocks.py", line 1340, in call_function
        prediction = await anyio.to_thread.run_sync(
                     ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
      File "/home/ben/mambaforge/envs/cfast/lib/python3.11/site-packages/anyio/to_thread.py", line 33, in run_sync
        return await get_asynclib().run_sync_in_worker_thread(
               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
      File "/home/ben/mambaforge/envs/cfast/lib/python3.11/site-packages/anyio/_backends/_asyncio.py", line 877, in run_sync_in_worker_thread
        return await future
               ^^^^^^^^^^^^
      File "/home/ben/mambaforge/envs/cfast/lib/python3.11/site-packages/anyio/_backends/_asyncio.py", line 807, in run
        result = context.run(func, *args)
                 ^^^^^^^^^^^^^^^^^^^^^^^^
      File "/home/ben/mambaforge/envs/cfast/lib/python3.11/site-packages/gradio/utils.py", line 759, in wrapper
        response = f(*args, **kwargs)
                   ^^^^^^^^^^^^^^^^^^
      File "/tmp/ipykernel_145374/855710716.py", line 10, in predict
        inp = transforms.ToTensor()(inp).unsqueeze(0)
              ^^^^^^^^^^^^^^^^^^^^^^^^^^
      File "/home/ben/mambaforge/envs/cfast/lib/python3.11/site-packages/torchvision/transforms/transforms.py", line 137, in __call__
        return F.to_tensor(pic)
               ^^^^^^^^^^^^^^^^
      File "/home/ben/mambaforge/envs/cfast/lib/python3.11/site-packages/torchvision/transforms/functional.py", line 140, in to_tensor
        raise TypeError(f"pic should be PIL Image or ndarray. Got {type(pic)}")
    TypeError: pic should be PIL Image or ndarray. Got <class 'NoneType'>

Back to top
