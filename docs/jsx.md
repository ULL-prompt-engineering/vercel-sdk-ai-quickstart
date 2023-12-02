
# JSX/TSX

JSX stands for JavaScript eXtended markup language. JSX is a syntax extension for JavaScript that allows you to describe your UI in a familiar HTML-like syntax. 
This code is JSX:

```tsx
(
    <div className="mx-auto w-full max-w-md py-24 flex flex-col stretch">
      <form onSubmit={handleSubmit}>
        <input
          className="fixed w-full max-w-md bottom-0 border border-gray-300 rounded mb-8 shadow-xl p-2 dark:text-black"
          value={input}
          placeholder="Describe your business..."
          onChange={handleInputChange}
        />
      </form>
      {completion ? (
        <div className="whitespace-pre-wrap my-4">{completion}</div>
      ) : (
        <div>Enter a business description and click enter to generate slogans.</div>
      )}
    </div>
  )
```

It’s possible to use TypeScript inside JSX using curly braces. 
The example below sets the `value` property  of the  `input` element
to the variable `input` and the `onChange` property to a function `handleInputChange` that updates the variable to the value written by the user inside the input box:

```jsx
      <form onSubmit={handleSubmit}>
        <input
          className="fixed w-full max-w-md bottom-0 border border-gray-300 rounded mb-8 shadow-xl p-2 dark:text-black"
          value={input}
          placeholder="Describe your business..."
          onChange={handleInputChange}
        />
      </form>
```

The nice thing about JSX is that apart from [following three JSX rules](https://beta.reactjs.org/learn/writing-markup-with-jsx#the-rules-of-jsx), you don’t need to learn any new symbols or syntax outside of HTML and JavaScript:

1. Return a single root element: To return multiple elements from a component, wrap them with a single parent tag.
2. Close all the tags: self-closing tags like `<img>` must become `<img />`
3. **camelCase** most of the things: For example, instead of `stroke-width` you use `strokeWidth`. Since `class` is a reserved word, in React you write `className` instead. Event names are also camelCased

