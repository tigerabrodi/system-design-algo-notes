# Browser Storages

In this post, we'll go over the different types of browser storages and how to use them.

# Cookies

Cookies are small pieces of data stored in the browser. They are sent with every request to the server, which can be used to e.g. identify a user.

Cookies have a size limit of 4KB and can be set to expire after a certain time. If you don't set an expiration date, the cookie will be deleted when the current session ends, which happens when the browser is closed.

Let's take a look at how to set a cookie in JavaScript:

```javascript
document.cookie = "name=John";
```

This will call the cookie's setter function and set the cookie "name" to "John". Because we haven't set an expiration date, this cookie will be deleted when the browser is closed.

Let's set another cookie:

```javascript
document.cookie = "age=30";
```

When we set a new cookie, it won't be deleted, but rather appended to the existing cookie string. So now, the cookie string will look like this: `name=John; age=30`.

## One string, different cookies

It may appear that we have only one cookie because `document.cookie` returns a single string. However, this string contains multiple cookies separated by a semicolon.

## Overriding cookies

To override a cookie, you can set it again with the same name. For example:

```javascript
document.cookie = "name=Jane";
```

The cookie "name" will now be set to "Jane".

## Expiration date

For each cookie, you can set an expiration date. The date must be in UTC format. For example, if we want the cookie "name" to expire right away:

```javascript
document.cookie = `name=John; expires=${new Date().toUTCString()}`;
```

This will set the expiration date to the current time in UTC which will cause the cookie to be deleted immediately.

## Max age

Another way to set an expiration date is by using the `max-age` attribute. This attribute specifies the number of seconds until the cookie expires. For example, if we want the cookie "name" to expire in 1 hour:

```javascript
document.cookie = `name=John; max-age=${60 * 60}`;
```

60 \* 60 seconds equals 1 hour. The name cookie will expire in 1 hour.

## Path

`path` specifies the URL path for which the cookie is valid. For example, if we want the cookie "name" to be valid only for the `/blog` path:

```javascript
document.cookie = `name=John; path=/blog`;
```

This can be useful if you want to restrict the cookie to a specific part of your website. But if you want the cookie to be valid for the entire website, you can set the path to `/`.

## Secure

`secure` ensures the cookie will only be sent over HTTPS connections. For example, if we want the cookie "name" to be secure:

```javascript
document.cookie = `name=John; secure`;
```

As you can see, it doesn't take any value. The presence of the attribute is enough to make the cookie secure.

## SameSite

`SameSite` helps prevent CSRF attacks by restricting when the cookie is sent.

It takes three possible values:

- `Strict`: The cookie will only be sent in a first-party context. This means the cookie will only be sent if the site is directly accessed.
- `Lax`: The cookie will be sent in a first-party context and in a cross-site context if the user navigates to the site from a link.
- `None`: The cookie will be sent in all contexts (never use this value unless you know what you're doing).

Many times, you'll want to set the `SameSite` attribute to `Lax`. This lets the cookie be sent in a cross-site context if the user navigates to the site from a link. However, if the external link or button is a malicious one making a POST request, the cookie won't be sent.

CSRF attacks are a big security risk, so it's important to set the `SameSite` attribute. They happen when a malicious website or element on a website sends a POST request to a legitimate website where the user is authenticated. If the user is logged in, the browser will send the cookies along with the request, which can lead to unauthorized actions.

For example, if you get an email with what appears to be a link to your bank's website, but it's actually a button that sends a POST request to your bank's website, the browser will send the cookies along with the request. If you're logged in, the bank's website will think you're making the request and will execute it.

Here is how to set the `SameSite` attribute:

```javascript
document.cookie = `name=John; SameSite=Lax`;
```

## Get a cookie

Let's say we want to get the "name" cookie:

```javascript
// Get all cookies -> ["name=John", "age=30"]
const cookies = document.cookie.split("; ");

// Find the "name" cookie
const nameCookie = cookies.find((cookie) => cookie.startsWith("name="));

// Get the value of the "name" cookie
// nameCookie is "name=John", so we split it by "=" and get the second element
const name = nameCookie.split("=")[1];
```

## HttpOnly

If you set the `HttpOnly` attribute, the cookie will only be accessible through HTTP requests. This means JavaScript won't be able to access it. This is useful for preventing XSS attacks.

You'll want to do this especially if you're sending sensitive information in the cookie from the server to the client.

## Recap

- Cookies have a size limit of 4KB.
- Cookies are sent with every request to the server.
- Cookies are small pieces of data stored in the browser.
- Cookies can be set to expire after a certain time, if not, they will be deleted when the browser is closed.

# Web Storage

`localStorage` and `sessionStorage` are both a part of the Web Storage API, which provides a way to store data in the browser. The data is stored as key-value pairs. The difference between localStorage and sessionStorage is that localStorage persists even after the browser is closed, while sessionStorage is deleted when the browser is closed.

Besides that, localStorage and sessionStorage have the same methods and properties.

An upside compared to cookies is that they can store more data. The limit is around 5MB, which is much more than the 4KB limit of cookies.

Some downsides to be aware of:

- Lack of expiration control.
- Not automatically sent with every request to the server.
- Potential for XSS attacks because the data is accessible through JavaScript. Therefore, you should never store sensitive information in them.

## The API

Let's take a look at how to use `localStorage`. That should be enough to understand `sessionStorage` as well.

```javascript
// Set an item
localStorage.setItem("name", "John");

// Get an item
const name = localStorage.getItem("name"); // "John"

// Remove an item
localStorage.removeItem("name");

// Clear all items
localStorage.clear();
```

One important thing to mention is that the data is stored as strings. So if you want to store objects or arrays, you'll need to convert them to strings first.

```javascript
const person = {
  name: "John",
  age: 30,
};

// Convert the object to a string
localStorage.setItem("person", JSON.stringify(person));

// Get the string and convert it back to an object
const personString = localStorage.getItem("person");

const person = JSON.parse(personString);
```

## Recap

- Web Storage API provides a way to store data in the browser.
- `localStorage` and `sessionStorage` are both part of the Web Storage API.
- `localStorage` persists even after the browser is closed, while `sessionStorage` is deleted when the browser is closed.
