# Origin Servers, CDNs and Edges 

## Origin Servers

The origin server refers to the main computer that stores and runs the original version of your application code. When an origin server receives a request, it does some computation before sending a response. **The result of this computation work can be moved to a CDN (Content Delivery Network)**.

## Content Delivery Network

CDNs store **static content** (such as HTML and image files) in multiple locations around the world and are placed between the client and the origin server. When a new request comes in, the closest CDN location to the user can respond with the cached result.

![cdn](https://sytws.netlify.app/images/cdn.png)

## The Edge

Edge servers are distributed to multiple locations around the world. Unlike CDNs, which store static content, Edge servers can run small snippets of code. Edge computing supports not only transmitting cached data but other types of computing like live streaming and gaming. 

## The Edge Runtime

The Edge Runtime is designed to help the  adoption of  **edge computing**. 
In the context of Next.js, [Edge runtime](https://nextjs.org/docs/app/building-your-application/rendering/edge-and-nodejs-runtimes) refers to the set of libraries, APIs, and general functionality available to your code during execution.

On the server, there are two runtimes where parts of your application code can be rendered:

- The **Node.js Runtime** (default) has access to all Node.js APIs and compatible packages from the ecosystem.
- The Edge Runtime is based on [Web APIs](https://nextjs.org/docs/app/api-reference/edge).

