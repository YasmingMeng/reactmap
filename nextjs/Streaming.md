## Streaming(流媒体)

- Streaming is a technique for transfer data,  it can be used for separate router into smaller chunks and stream them one by one from the server to  the client when it ready to load.

- Streaming can prevent the whole page block because the slow data fetch.

![Diagram showing time with sequential data fetching and parallel data fetching](https://nextjs.org/_next/image?url=%2Flearn%2Fdark%2Fserver-rendering-with-streaming-chart.png&w=3840&q=75)

- In react components model, every component consider as a small chunk.
- In nextJs there has two way to implement Streaming:
  1. At the page level, with the `loading.tsx` file.
  2. For specific components, with `<Suspense>`.

- which situation should be place `suspense` boundaries

  - the good practice to move the fetch data down to the components where need it.

    