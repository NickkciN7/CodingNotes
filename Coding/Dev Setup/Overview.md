- [[lerna and root directory]]
- [[Start App and Command Line Interface (CLI)]] to make backend
- [[Making and starting React]] to make frontend (Vite)
- [[Eslint and Prettier]] in root, frontend, and backend. reuse root settings
- Add this to `backend/src/main.ts` before `app.listen` to enable fetching from front end with fetch.
- http://127.0.0.1:5173 is vite server default
- http://localhost:3000 is npx create-react-app server one
	- note that nest.js defaults to port 3000 too, so need to change `app.listen(3000)` to 8000 in main.tsx in backend.
```
app.enableCors({
    origin: ['http://127.0.0.1:5173', 'http://localhost:3000'], // Allow only your frontend URL
    methods: ['GET', 'POST', 'PUT', 'DELETE', 'PATCH', 'OPTIONS'], // Allowed methods
    allowedHeaders: ['Content-Type', 'Authorization'], // Allowed headers
    credentials: true, // Allow cookies if you need them
  });
```
- fetch. the useEffect with the empty [] at the end basically means run useEffect only once when the component renders. the [] can contain dependencies that will cause useEffect to run when they change. But an empty array [] means only run once. not necessary to use useEffect to use fetch though
```
useEffect(() => {
    fetch('http://localhost:8000/')
      .then((response) => response.text())
      .then((data) => console.log(data))
      .catch((error) => console.error('Error:', error));
  }, []);
```