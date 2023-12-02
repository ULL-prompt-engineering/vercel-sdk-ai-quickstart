## Streaming

Large Language Models (LLMs) are extremely powerful. However, when generating long outputs, they can be very slow compared to the latency you're likely used to. If you try to build a traditional blocking UI, your users might easily find themselves staring at loading spinners for 5, 10, even up to 40s waiting for the entire LLM response to be generated. This can lead to a poor user experience, especially in conversational applications like chatbots. Streaming UIs can help mitigate this issue by displaying parts of the response as they become available.

### OpenAIStream

[OpenAIStream](https://sdk.vercel.ai/docs/api-reference/openai-stream) is a utility function that transforms the `response` from OpenAI's completion and chat models into a [ReadableStream](https://nodejs.org/api/webstreams.html#class-readablestream). 

It uses [AIStream](https://sdk.vercel.ai/docs/api-reference/ai-stream) under the hood, applying a specific parser for the OpenAI's response data structure.

It is designed to work with responses from either 

- [openai.completions.create](https://platform.openai.com/docs/guides/text-generation/completions-api) or 
- [openai.chat.completions.create](https://platform.openai.com/docs/guides/text-generation/chat-completions-response-format) 

The `OpenAIStream` function has the following signature:

```ts
OpenAIStream(res: Response, cb?: AIStreamCallbacks)
```

The parameters are:

- `res: Response`. This is the response object returned by either `openai.completions.create` or `openai.chat.completions.create` methods.
- `cb?: AIStreamCallbacks`. This is an optional parameter which is an object that contains callback functions for handling the start, completion, and each token of the AI response. If not provided, default behavior is applied.

```ts
import { OpenAIStream, StreamingTextResponse } from 'ai';

export async function POST(req: Request) {
  const { prompt } = await req.json();
 
  const response = await openai.completions.create({ 
    stream: true, model: 'text-davinci-003', temperature: 0.6,  max_tokens: 300, 
    prompt: `Create three slogans ...Business: ${prompt} Slogans:` });
  const stream = OpenAIStream(response);
  return new StreamingTextResponse(stream);
}
```

## StreamingTextResponse

[StreamingTextResponse](https://sdk.vercel.ai/docs/api-reference/streaming-text-response) is a utility class that simplifies the process of returning a [ReadableStream](https://nodejs.org/api/webstreams.html#class-readablestream) of text in HTTP responses. It is a lightweight wrapper around the native Response class, automatically setting 
- the status code to `200` and 
- the `Content-Type` header to `'text/plain; charset=utf-8'`.

Its constructor has the following signature:

```ts
StreamingTextResponse(res: ReadableStream, init?: ResponseInit): Response
```

For instance:

```ts
// app/api/generate/route.ts
import { OpenAIStream, StreamingTextResponse } from 'ai';
 
export const runtime = 'edge';
 
export async function POST() {
  const response = await openai.chat.completions.create({
    model: 'gpt-4',
    stream: true,
    messages: [{ role: 'user', content: 'What is love?' }],
  });
  const stream = OpenAIStream(response);
  return new StreamingTextResponse(stream, {
    headers: { 'X-RATE-LIMIT': 'lol' },
  });
  // Returns a Response with the stream as the body,
  // status code 200,
  // and headers 'Content-Type': 'text/plain; charset=utf-8' and 'X-RATE-LIMIT': 'lol'.
}
```

It takes two parameters:

- `res: ReadableStream`.  This parameter should be a `ReadableStream` which represents the content of the HTTP response.
- `init?: ResponseInit`. This optional parameter can be used to customize the properties of the HTTP response. It is an object that corresponds to the `ResponseInit` object used in the Response constructor.

The `ResponseInit` object can contain the following properties:

- `status?: number`: The status code for the response. `StreamingTextResponse` will overwrite this value with 200.
- `statusText?: string`: The status message associated with the `status` `code`.
- `headers?: HeadersInit`: Any headers you want to add to your response. `StreamingTextResponse` will add `'Content-Type': 'text/plain; charset=utf-8'` to these headers.
