# Serverless Functions

[A **serverless** function](https://vercel.com/docs/functions/serverless-functions), see also [^1]  is a piece of code that is executed in response to a specific event, such as an HTTP request or a message being added to a queue. It is called "*serverless*" because the developer does not have to worry about the underlying infrastructure that the code will be running on. Instead, the infrastructure is managed by a third party, such as AWS Lambda or Google Cloud Functions. 

The developer only needs to provide the code and specify the events that should trigger the code to be executed. The **serverless provider** takes care of the rest, including automatically scaling the function to handle a large number of requests.

![https://sytws.netlify.app/images/how-do-serverless-functions-work.png](https://sytws.netlify.app/images/how-do-serverless-functions-work.png)

![https://vercel.com/_next/image?url=https%3A%2F%2Fassets.vercel.com%2Fimage%2Fupload%2Fv1689795055%2Fdocs-assets%2Fstatic%2Fdocs%2Fconcepts%2Ffunctions%2Fedge-functions-light.png&w=3840&q=75&dpl=dpl_9popvVXyaYTHjAgsjnyhAr6SgWMX](https://vercel.com/_next/image?url=https%3A%2F%2Fassets.vercel.com%2Fimage%2Fupload%2Fv1689795055%2Fdocs-assets%2Fstatic%2Fdocs%2Fconcepts%2Ffunctions%2Fedge-functions-light.png&w=3840&q=75&dpl=dpl_9popvVXyaYTHjAgsjnyhAr6SgWMX)

[^1]: [Serverless Functions](https://sytws.netlify.app/temas/web/serverless.html#serverless-functions)