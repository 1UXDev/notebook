# Backend Update

General Things about the Methods:


**Two ways to alter data (except Delete and Create)**
* Put: provide whole object
* Patch: Specify Certain property of record

<br>

**Put:**
 the findbyIdAndUpdate method has a second argument that defines what it does. These argument start with "$" - for updating it would be $set
```jsx
await Product.findByIdAndUpdate(id, {
      $set: request.body,
    });
```

<br>

**Delete:**
`await Product.findByIdAndDelete(id);`

<br>

**Get**
```jsx
await dbConnect();
  const { id } = request.query;

  if (request.method === "GET") {
    const product = await Product.findById(id).populate("reviews");

    if (!product) {
      return response.status(404).json({ status: "Not Found" });
    }

    response.status(200).json(product);
  }
```

<br>

**POST**

```jsx 
if (request.method === "POST") {
    try {
      const productData = request.body;
      const product = new Product(productData);
      await product.save();
      return response.status(201).json({ status: "Product created." });
    } catch (error) {
      console.error(error);
      return response.status(400).json({ error: error.message });
    }
  }

```


-> 
```Product.findByID(id).populate("reviews")``` Defines that Product has relations to Reviews, and Updates / Gets them accordingly

*Sidenotes*
* Every Statuscode starting with 4 is on the client-side
* Errorcode starting with 5 is on server side
* 201 is for create-Ressource

<br>

<br>

----------------

<br>



# Backend Update and Delete

## Learning Objectives

- [ ] Understanding the Update and Delete part of CRUD operations
- [ ] Being able to implement `UPDATE` and `DELETE` API routes

---

## Update

To update an entry in your database, you need to do two things:

- define a `PUT` API route and
- connect the submit handler of an edit form to this API route.

### Update with Mongoose

First, define a `PUT` API route:

```js
// /api/jokes/[id].js
if (request.method === "PUT") {
  const jokeToUpdate = await Joke.findByIdAndUpdate(id, {
    $set: request.body,
  });
  // Find the joke by its ID and update the content that is part of the request body!
  response.status(200).json(jokeToUpdate);
  // If successful, you'll receive an OK status code.
}
```

### `PUT` using `fetch`

Second, tell the submit handler of your edit form

- to use the `PUT` API route (i.e. send a request to your database to edit an entry),
- wait for the database to respond and update the UI if necessary or
- navigate the user to a different page via `push()`.

> 💡 Note: `PUT` and `PATCH` are semantically different. According to convention, we would use `PUT` to update our entire document, and `PATCH` to update individual fields. In our demo, we're using `PUT`, simply because we only ever have _one_ field to update.

You can [use the `useSWRMutation` hook](https://swr.vercel.app/docs/mutation#useswrmutation) to achieve this.

Go to the `page` or `component` where you want to write the submit handler of your edit form.

Import `useSWRMutation` and destructure the `trigger` method and the `isMutating` state:

```js
// pages/[id].js
import useSWRMutation from "swr/mutation";

export default function JokeDetailsPage() {
  //...
  const { trigger, isMutating } = useSWRMutation(
    `/api/jokes/${id}`,
    sendRequest
  );
  // return (...)
}
```

The second argument passed to `useSWRMutation`, the `sendRequest`, is a function you need to write. It is a wrapper function for `fetch` and will be called whenever you call `trigger()`.

Note that it is here where you define the `PUT` method and the `body` for your API route:

```js
// pages/[id].js

async function sendRequest(url, { arg }) {
  // The sendRequest function expects url and { arg } as parameters.
  // This naming convention isn't unintentional. It needs to be named like that.
  // This has to do with how useSWRMutation works.
  const response = await fetch(url, {
    method: "PUT",
    body: JSON.stringify(arg),
    headers: {
      "Content-Type": "application/json",
    },
  });
  // This syntax follows that of any regular HTTP response.
  // Note the arg object that is passed as part of the response body.
  if (response.ok) {
    await response.json();
  } else {
    console.error(`Error: ${response.status}`);
  }
}
```

You now need to write a function that provides your `sendRequest` function with the `arg` object:

```js
// pages/[id].js

async function handleEditJoke(event) {
  event.preventDefault();
  const formData = new FormData(event.target);
  const jokeData = Object.fromEntries(formData);
  // Here you are preparing your updated data to be handed over to your sendRequest function.
  await trigger(jokeData);
  // By calling trigger with our jokeData object, you provide your `sendRequest` function with the necessary `arg` object.
  push("/");
}
```

If you want to redirect to the homepage with `push("/")`, you need to destructure the `push` method from the `useRouter` hook at the top of your component:

```js
// pages/[id].js
export default function JokeDetailsPage() {
  const router = useRouter();
  const {
    query: { id },
    push,
  } = router;
}
```

Summary:

- `trigger` informs `useSWRMutation` about `jokeData`,
- then `isMutating` evaluates to `true` and
- `useSWRMutation` hands over `jokeData` to `sendRequest`
- which accepts it as the `{ arg }` object
- and then sends this `{ arg }` object down your API route as part of your response body.
- Now, `isMutating` evaluates to `false`.
- Once all of this has happened, you're safe to push to your overview page (or any other page).

### Render while `isMutating`

If you want to inform the user that the changes are currently being submitted, you can make use of `isMutating`. Simply add an early return to your component:

```js
// pages/[id].js
if (isMutating) {
  return <h1>Submitting your changes...</h1>;
}
```

> 📙 [Read more about `useSWRMutation` in the swr docs](https://swr.vercel.app/docs/mutation#useswrmutation).

---

## Delete

To delete an entry in your database, you need to do two things:

- define a `DELETE` API route and
- connect a handler function which uses this API route.

### Delete with Mongoose

First, define a `DELETE` API route:

```js
if (request.method === "DELETE") {
  const jokeToDelete = await Joke.findByIdAndDelete(id);
  // Declare jokeToDelete to be the joke identified by its id and delete it.
  // This line handles the entire deletion process.
  response.status(200).json(jokeToDelete);
}
```

### `DELETE` using `fetch`

Second, write a handler function which calls `fetch()` with the appropriate arguments and pass it to a delete button:

```jsx
async function handleDeleteJoke() {
  await fetch(`/api/jokes/${id}`, {
    method: "DELETE",
  });
  // You are handing over the joke identified by its id to our DELETE request method.
  // This is the entire code required to do so.
  push("/");
  // After deleting the joke, you route back to our index page.
}

return (
  <button type="button" onClick={() => handleDeleteJoke()}>
    Delete
  </button>
);
```

---

## Resources

- [useSWRMutation (SWR Docs)](https://swr.vercel.app/docs/mutation#useswrmutation)
