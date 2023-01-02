## Axios 쓰는 법 3가지

```js
axios({
  method: "post",
  url: REFRESH_TOKEN_URL,
  data: params,
  headers: {
    Authorization: "Basic " +
                    Buffer.from(SPOTIFY_CLIENT_ID + ":" + SPOTIFY_SECRET_ID).toString(
"base64"
),
  "Content-Type": "application/x-www-form-urlencoded",
},
})
```

```js
// Axios 공식 Docs
axios.post('/user', { firstName: 'Fred', lastName: 'Flintstone' }) .then(function (response) { console.log(response); }) .catch(function (error) { console.log(error); });
```

