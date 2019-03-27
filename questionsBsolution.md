# Interview Prep Questions (B)

1. What is CRUD? Give a brief overview of how you can create a CRUD API.

CRUD (Create, Read, Update, and Delete) are the four basic functions that a model should be able to do, at most.

The CRUD paradigm is common in constructing web applications, because it provides a memorable framework for reminding developers of how to construct full, usable models.

For example, let's imagine a system to keep track of library books. In this hypothetical library database, we can imagine that there would be a books resource, which would store book objects. Let's say that the book object looks like this:

```json
"book": {
  "id": <Integer>,
  "title": <String>,
  "author": <String>,
  "isbn": <Integer>
}
```

To make this library system usable, we would want to make sure there were clear mechanisms for completing the CRUD operations.

- **Create**: This would consist of a function whch we would call when a new library book is being added to the catalog. The program calling the function would supply the value for `title`, `author`, and `isbn`. After this function is called, there should be a new entry in the books resource corresponding to this new book. Additionally, the new entry is assigned a unique `id`, which can be used to access this resource later.

- **Read**: This would consist of a function which would be called to see all of the books currently in the catalog. This function call would not alter the ooks in the catalog &mdash; it would simply retrieve the resource and display the results. We would also have function to retrieve a single book, for which we could supply the `title`, `author`, or `isbn`. Again, this book would not be modified, only retrieved.

- **Update**: There should be a function to call when information about a book must be changed. The program calling the function would supply the new values for `title`, `author`, and `isbn`. After the function call, the corresponding entry in the books resource would contain the new fields supplied.

- **Delete**: There should be a function to call to remove a library book from the catalog. The program calling the function would supply one or more values (`title`, `author`, and/or `isbn`) to identify the book, and then this book would be removed from the books resource. After this function is called, the books resource should contain all of the books it had before, except for the one just deleted.

In a REST environment, CRUD often corresponds to the HTTP methods `POST`, `GET`, `PUT`, and `DELETE`, respectively. These are the fundamental elements of a persistent storage system.

Imagine we are working with a system that is keeping track of meals and their corresponding prices for a restaurant. Let’s look at how we would implement CRUD operations.

- **Create**: To create resources in a REST environment, we most commonly use the HTTP `POST` method. `POST` creates a new resource of the specified resource type. Upon successful creation, the server should return a header with a link to the newly-created resource, along with a HTTP response code of `201 (CREATED)`.

- **Read** To read resources in a REST environment, we use the `GET` method. Reading a resource should never change any information - it should only retrieve it. If you call `GET` on the same information 10 times in a row, you should get the same response on the first call that you get on the last call. `GET` requests can also be used to read a specific item, when its `id` is specified in the request. After this request, no information has been changed in the database. When there are no errors, `GET` will return the HTML or JSON of the desired resource, along with a `200 (OK)` response code. If there is an error, it most often will return a `404 (NOT FOUND)` response code.

- **Update** `PUT` is the HTTP method used for the CRUD operation, Update. The response includes a Status Code of `200 (OK)` to signify that the operation was successful, but it need not return a response body.

* **Delete** The CRUD operation Delete corresponds to the HTTP method `DELETE`. It is used to remove a resource from the system. Such a call, if successful, returns a response code of `204 (NO CONTENT)`, with no response body.

---

2. Explain the same-origin policy and how it relates to CORS.

Although you may not notice it, the web pages you visit make frequent requests to load assets like images, fonts, and more, from many different places across the Internet. If these requests for assets go unchecked, the security of your browser may be at risk. For example, your browser may be subject to hijacking, or your browser might blindly download malicious code. As a result, many modern browsers follow security policies to mitigate such risks.

The same-origin security policy is very restrictive. Under this policy, a document (i.e., like a web page) hosted on server A can only interact with other documents that are also on server A. In short, the same-origin policy enforces that documents that interact with each other have the same origin.

A request for a resource (like an image or a font) outside of the origin is known as a cross-origin request. CORS (cross-origin resource sharing) manages cross-origin requests. Allowing cross-origin requests is helpful, as many websites today load resources from different places on the Internet (stylesheets, scripts, images, and more).

Cross-origin requests, however, mean that servers must implement ways to handle requests from origins outside of their own. CORS allows servers to specify who (i.e., which origins) can access the assets on the server, among many other things.

The CORS standard is needed because it allows servers to specify not just who can access its assets, but also how the assets can be accessed.

Cross-origin requests are made using the standard HTTP request methods. Most servers will allow `GET` requests, meaning they will allow resources from external origins (say, a web page) to read their assets. HTTP requests methods like `PATCH`, `PUT`, or `DELETE`, however, may be denied to prevent malicious behavior. For many servers, this is intentional.

With CORS, a server can specify who can access its assets and which HTTP request methods are allowed from external resources. The CORS standard manages cross-origin requests by adding new HTTP headers to the standard list of headers.

---

3. What is destructuring? Can you give me an example of destructuring an array and an object? How do I destructure function parameters?

The destructuring assignment syntax is a JavaScript expression that makes it possible to unpack values from arrays, or properties from objects, into distinct variables.

Example: Basic array destructuring

```js
var foo = ['a', 'b', 'c'];
var [one, two, three] = foo;
console.log(one); // 'a'
console.log(two); // 'b'
console.log(three); // 'c'
```

Example: Basic object destructuring

```js
var o = { p: 42, q: true };
var { p, q } = o;
console.log(p); // 42
console.log(q); // true
```

Example: Unpacking fields from objects passed as function parameter

```js
var user = {
  id: 42,
  displayName: 'jdoe',
  fullName: {
    firstName: 'John',
    lastName: 'Doe',
  },
};

function whois({ displayName, fullName: { firstName: name } }) {
  console.log(displayName + ' is ' + name);
}

whois(user); // "jdoe is John"
```

---

4. What is an ES6 template literal? What problem do they solve?

Template literals are string literals allowing embedded expressions. You can use multi-line strings and string interpolation features with them. They were called "template strings" in prior editions of the ES2015 specification.

---

5. Can you give an example of a template literal in use?

Example: Multi-line strings

```js
console.log(`string text line 1\n` + `string text line 2`);
// "string text line 1
// string text line 2"
```

Example: Expression interpolation

```js
var a = 5;
var b = 10;
console.log(`Fifteen is ${a + b} and
not ${2 * a + b}.`);
// "Fifteen is 15 and
// not 20."
```

---

6. How do you calculate the "length" of an object (i.e. the number of keys)

```js
Object.keys(myObj).length;
```

---

7. What will be the output of this code?

```js
for (var i = 0; i < 10; i++) {
  setTimeout(function() {
    console.log(i);
  }, 1000);
}
```

Answer:

```txt
10
10
10
10
10
10
10
10
10
10
```

---

8. Follow-up: How can we fix this to output 0, 1, 2, 3, 4 ...

Answer:

```js
for (let i = 0; i < 10; i++) {
  setTimeout(function() {
    console.log(i);
  }, 1000);
}
```

---

9. Write a function duplicate that takes an array and returns a new array containing each element twice.

Example:

```js
duplicate([1, 2, 3, 4]); // [1, 1, 2, 2, 3, 3, 4, 4]
```

Answer:

```js
function duplicate(arr) {
  let duplicates = [];

  for (let i = 0; i < arr.length; i++) {
    duplicates.push(arr[i]);
    duplicates.push(arr[i]);
  }

  return duplicates;
}
```

10. Bonus: return an array where the amount of each element in the returned array is its index in the original

Example:

```js
duplicate([1, 2, 3, 4]); // [2, 3, 3, 4, 4, 4]
```

Answer:

```js
function duplicate(arr) {
  let duplicates = [];

  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < i; j++) {
      duplicates.push(arr[i]);
    }
  }

  return duplicates;
}
```

11. Can you describe the main difference between a .forEach loop and a .map loop and why you would pick one versus the other?

The `forEach()` method executes a provided function once for each array element.

The `map()` method creates a new array with the results of calling a provided function on every element in the calling array.

Since map builds a new array, using it when you aren't using the returned array is an anti-pattern.

---

12. Explain event bubbling

Event bubbling is a type of event propagation where the event first triggers on the innermost target element, and then successively triggers on the ancestors of the target element in the same nesting hierarchy till it reaches the outermost DOM element or document object.
