# LinkedIn Larp Translator

Paste a long, "humbled and honored" LinkedIn post. Get the one-line truth.

**Live demo:** <!-- paste your Vercel or GitHub Pages link here --><img width="855" height="882" alt="image" src="https://github.com/user-attachments/assets/283119ba-47b6-485f-b510-838e1dda7ee1" />


## What it does

You paste a post like this:

> After 7 incredible years, I'm humbled and honored to share that I've decided to embark on a new chapter. This journey taught me so much about leadership and resilience. Grateful to everyone who believed in me. Stay tuned! #newbeginnings

You get one short line back, something like:

> Quit their job.

That's the whole app: one page, one job, no extra information.

## Why I built it

<!-- Replace this with your own story: who is the friend, and what was their problem? Example: "My friend X spends hours scrolling LinkedIn for job leads and gets worn out reading 300-word posts that say one thing." If they tried it, add a quote from them. -->

## Why open source matters here

- **Private by default.** The model runs on your own device, so nothing you paste is sent anywhere.
- **Free to run and host.** There's no per-request bill and no API key. The whole app is one static HTML file.
- **Swappable models.** The dropdown switches between Qwen 2.5 1.5B, Llama 3.2 1B and Llama 3.2 3B. Adding another model is a one-line change.
- **Tweakable behavior.** The prompt and the example translations sit in a config block at the top of the file, so you can change how it talks without retraining anything.
- **Works offline after the first load.** Once a model is downloaded and cached, you can use it without a connection.

## How it works

- **[WebLLM](https://github.com/mlc-ai/web-llm)** runs open-weight models in the browser using WebGPU for hardware acceleration.
- A short **system prompt** asks for exactly one sentence under 20 words.
- **Four worked examples** (long post in, one-liner out) are sent with every request. Small models follow a pattern much better when they are shown it.
- A small **cleanup step** keeps only the first line and first sentence, and removes labels and quote marks the model sometimes adds.
- The AI library loads from several CDNs in turn, so one blocked source doesn't break the page.

## Run it yourself

1. Download `index.html`.
2. Open it in a recent **Chrome or Edge** on a laptop. Browsers that lack WebGPU won't work.
3. Paste a post and click **Translate**.

The first run downloads the model (about 0.7 to 2 GB depending on the model you pick) and caches it, so later runs start much faster.

If opening the file directly gives download errors, serve it over http instead:

```bash
python -m http.server 8000
# then open http://localhost:8000
```

Don't open it inside an editor or chat-app preview. Previews block the model download. The **Check connection** button on the page tests each download step and shows which one fails.

## Deploy it

It's a single static file, so any static host works.

- **Vercel:** push this repo to GitHub, import it at vercel.com, set the framework preset to **Other**, and deploy.
- **GitHub Pages:** Settings, then Pages, then deploy from the `main` branch root.

## Customize it

Everything you'd want to change is in the `CONFIG` block near the top of the script in `index.html`:

| Setting | What it changes |
| --- | --- |
| `models` | The models offered in the dropdown. Any model ID from WebLLM's prebuilt list works. |
| `systemPrompt` | The instructions the model follows. |
| `examples` | The worked examples. Add one for any style of post it gets wrong. |
| `temperature`, `maxTokens` | How varied the output is, and how long it can be. |

## Limitations

- A small model can misread a post or miss sarcasm, so treat the gist as a quick guess.
- It needs a browser with WebGPU. Phones are less reliable than laptops.
- The first load is a big download.
- It only reads the text you paste. It doesn't fetch posts from LinkedIn.

## Credits

- [WebLLM](https://github.com/mlc-ai/web-llm) by the MLC team.
- Open-weight models from Meta (Llama) and Alibaba (Qwen). Each model has its own license, so check them before reusing the models commercially.

## License

<!-- Add a LICENSE file (MIT is a simple choice) and name it here. -->


https://linkedin-larp-translator.vercel.app/
