# AI in plain HTML and JavaScript (ChatGPT-style, no backend)

One HTML file that sends a prompt to an AI model and streams the answer onto the page, with chat history. No server, no build step, and no secret key in the page.

**Live demo:** https://fengyiqicoder.github.io/chatgpt-api-html-js/

## Why not call the ChatGPT API directly?

An OpenAI API key is a secret: put it in front-end JavaScript and anyone can copy it from View Source or DevTools and spend your money. This page uses a [OneTag AI](https://onetagai.com) key instead, which is public by design: it can only call one AI endpoint, with a token limit, so it is safe to ship in the page.

The answers come from OneTag AI, not from OpenAI or ChatGPT. This project is not affiliated with OpenAI.

## Use it

1. Get a free key at [onetagai.com](https://onetagai.com) (1,000,000 tokens one time, no credit card).
2. In `index.html`, replace the demo key `ot_demo000000000000000000000` with yours.
3. Open the page, or put it on any static host (GitHub Pages, Netlify, Cloudflare Pages).

## The JavaScript

```js
const history = [];
const text = await onetag.ask(prompt, null, {
  system: "You are a helpful assistant. Reply in plain text, no Markdown.",
  history,                                        // earlier turns, so follow-ups work
  stream: (delta) => (answer.textContent += delta), // show the answer as it is written
});
history.push({ role: "user", content: prompt }, { role: "assistant", content: text });
```

All options (`system`, `maxTokens`, `json`, `signal`) are in the [docs](https://onetagai.com/docs).

## License

MIT
