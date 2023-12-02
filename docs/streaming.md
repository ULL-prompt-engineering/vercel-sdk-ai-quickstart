## Streaming

Large Language Models (LLMs) are extremely powerful. However, when generating long outputs, they can be very slow compared to the latency you're likely used to. If you try to build a traditional blocking UI, your users might easily find themselves staring at loading spinners for 5, 10, even up to 40s waiting for the entire LLM response to be generated. This can lead to a poor user experience, especially in conversational applications like chatbots. Streaming UIs can help mitigate this issue by displaying parts of the response as they become available.

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

### OpenAIStream

`OpenAIStream` is a utility function that transforms the `response` from OpenAI's completion and chat models into a [ReadableStream](https://nodejs.org/api/webstreams.html#class-readablestream). It uses [AIStream](https://sdk.vercel.ai/docs/api-reference/ai-stream) under the hood, applying a specific parser for the OpenAI's response data structure.

See [OpenAIStream](https://sdk.vercel.ai/docs/api-reference/openai-stream) for more details.

[StreamingTextResponse](https://sdk.vercel.ai/docs/api-reference/streaming-text-response) is a helper class that takes an `OpenAIStream` and returns a `Response` object that can be returned from a Next.js route handler.