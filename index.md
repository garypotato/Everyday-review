# 03/09/2023:

- JavaScript
  - understand the regx: /-\$?\d+(\.\d+)?/g;
  - closure:
    - a function (b) return by another function (a)
    - function b will have a closure that includes all the variables when function b is created
  - this:
    - refers to the last object
- Next.js
  - pre-rending:
    - make app render faster
    - SEO
  - different types of pages:
    - `Static`: automatically rendered as static HTML
    - `SSG`: automatically rendered as a static HTML + JSON
    - `ISR`: incremental static regeneration
  - client component: **Hydration**
    - static HTML will be render from sever
    - the browser display the HTML from server, and also load the JS files and make the element can be interactive
  - deployment:
    - vercel: deploy same with AWS Amplify
    - Netlify:
      - local:
        - 'npx run build' & 'npx next export -o dist'
        - test it at 'npx serve dist'
      - netlify:
        - drag the 'dist' file in
    - nginx server:
      - install nginx in the Linux(for example)
      - copy all the files under `dist` and paste to `var/ww/html` in `nginx`
- Tailwind:
  - A utility-first CSS framework packed with classes like flex, pt-4, text-center and rotate-90 that can be composed to build any design, directly in your markup.
- strapi:
  - headless CMS
  - run it locally
  - provide UI for collection creation, etc
  - automatically generate REST APIs for data querying

# 04/09/2023

- Hasura:
  - same query can pop up a couple time, but need to nest it. For example:
    `AllPropertyView: {
\_or: [{AllPropertyViewID: {\_in: [123456]}}, {AllPropertyView_PropertyLotStrata: {eacPropkey: {\_in:[98765543]}}}],
AllPropertyView_PropertyLotStrata: {eacPropkey:{\_in:[98765543,9876543]}}
}`
- Next.js
  - incremental static regeneration: `getStaticProps`
    - the browser request the HTML and nextjs server return the old HTML to browser and doesn't wait the new data arrive
    - but in the background, it will re-generate the page with the new data
    - refresh one more time, the new HTML with updated data will be displayed
    - it will re-fetch the data when expired no matter if the data updated
    - can't `npx next export`
  - Lambda: `getServerSideProps`
    - server-side rendered but at runtime
    - it will run in `dev` mode
  - `getStaticProps` vs `getServerSideProps`
    - depends on if latest data need to be displayed
  - API routes
    - API routes provide a solution to build a public API with Next.js.
    - Any file inside the folder pages/api is mapped to /api/\* and will be treated as an API endpoint instead of a page.
    - can formate the data before sending to client
  - data fetching:
    - static generation: `getStaticProps`
      - static HTML generated when build and data remain unchanged
    - incremental static regeneration: `getStaticProps` + `revalidate`
      - will re-generated the HTML periodically
    - server-side rendering: `getServerSideProps`
      - always get the latest data
    - client side fetch
      - client directly fetch the data from backend
    - client side fetch + next.js API routing
      - browser doesn't need to access the backend api

# 05/09/2023

- Next.js
  - on-demand Revalidation
    - create a next.js server api in /pages/api/revalidation for example
    - in `CMS` create a webhook, that will request `xxx/api.revalidation`
    - nest.js server receive the request and handle the logic
  - fallback: blocking
    - if the dynamic path is no exist in the **build time**, for example new product with new id.
    - next.js generate a new page
  - page not found handling
  - environment variables
    - `.env` for production
    - `.env.local` for local, will overwrite `.env` when run in local

# 06/09/2023

- Product Fruits
  - similar with 'chat now', manage user feedback
- daily development
  - always remember to handle `fetch error` and `undefined`
- delete `cookie`
  - set an empty cookie with expired time(previous time)
- `React Query`
  - use the combination of the `cache` and `staleTime` sometime doesn't need `Redux`
  - `queryClient.setQueryData()` to force cache update

# 09/09/2023

- Next.js
  - `app router` vs `page router`
    - `app router` includes `server component` and `client component`
    - `server component` only runs in server, means no extra JS code send to browser; only can use server side functionality
    - `client component` pre-render in server and re-render in the browser for client functionality
    - `page router` always run twice, first `server` then `browser`
  - `<Link>`
    - by default, the next.js app is multi-page app
    - every time the route change, it will render a new page
    - `<Link>` make the app similar to `SPA` and use the client side navigation
  - `pre-fetching`:
    - happened in `production mode`
    - pre-fetches all links right after loading the initial page
    - disabled: add `prefetch={false}` to `<Link>`
  - `Google font`
    - `next.js` will automatically download the font files as static asset when `build`, that web page doesn't need to send request to Google for fonts
  - `dangerouslySetInnerHTML`
    - can display html code directly
    - think carefully before use: if insert the html code entered by user, that user can add `<script />` tag and run js code.
  - `markdown`
    - npm `marked`: read the `markdown` file
    - npm `Tailwind CSS Typography`: insert the html to `<article/>` with format
    - npm `gray-matter`: allow `markdown` attach addition information

# 10/09/2023

- Next.js
  - `dynamic routes`
    - by default, it's **server-side renders** at runtime, it's **no static page**
      - if re-render the dynamic page, the server will re-generate the HTML and sent to the browser
      - downside: **slower** than static page
    - how to fix？`generateStaticParams()`
      - when **build**, `slug` shows `SSG`
  - `Metadata`
    - for example: `title`
      - suggest to add in `layout.js`
      - `title template`
    - `dynamic metedata`
      - `generateMetadata()`
  - `icon`
    - Add a favicon.ico image file to the root /app route segment. **Next.js** will handle for u
  - `client component`
    - `Hydration`
    - when the **next component** is `client component`, the parent component doesn't need to specific **client component**
    - only specific **client component** when necessary
  - `heroicons`
    - same team with `Tailwind`
  - `Headless CMS`:
    - what's that?: focus on **data management** and **provide APIs**
    - vs `traditional CMS`:
      - **traditional CMS** manage and present the data are attached to each other
      - **Headless CMS** doesn't care the UI and how to present data
    - vs `backend server`
      - **server** also need to care the logic of a project, eg. authorisation and authentication

# 11/09/2023

- Strapi
  - **populate and select**: it has something similar to `GraphQL`, can request the fields u need
- Next.j
  - `<Image/>`
  - `Route Segment Config`
    - `dynamicParams`: if `generateStaticParams()` presents, set `dynamicParas` to false will disable the unknown dynamic route
    - `dynamic`
      - `force-dynamic`
        - always fetching the latest updates
        - dirty and quick
        - force every page re-rend in run time
  - Background revalidation
  - fetch api
    - set **cache** to no store will have similar behavior with `force-dynamic`
    - set **revalidate** will have the similar behavior with `background revalidation`
  - next/navigation
    - redirect to `404`
    - `notFound()`
    - or create not found page under `/app`
  - on-demand revalidation
    - webhook

# 12/09/2023

- Next.js
  - `searchParams` is dynamic API, will opt the page into **dynamic rendering**
    - example: `/reviews?page=2`
  - third party npm:
    - it will always have issue that a same component from the server is different from the browser
      - e.g. text (id) different
  - pass data from `server component` to `client component`
    - fetch the data in the build time will increase the size the pages (sever component), especially when the data will grow
    - only suggest when there is a fixed amount of data,
  - handler: create handler not to expose the api to public
    - act like a proxy
  - fetch (next.js)
    - can be happen both in client and server
    - `server-only npm` can limit the fetch usage in **server** only
  - env
    - different name of environment variable in **server** and **client**
    - `next.config.js` can also read the env
- JavaScript
  - `encodeURIComponent` before formatting the url
  - `new URL()`
  - `AbortController` cancel request
  - `debounce`: **use-debounce npm**
- React
  - `useEffect`: react will first call the cleanup function returned by the previous `userEffect` invocation, so any previous fetch request will be cancelled.
  - can **redirect** the url before the react app mount to the html, that means
    - before the **Redux** initialized
    - before hitting the **react-router**

# 13/09/2023

- MSSQL & hasura
  - upsert data in hasura, **if match** can't includes the columns that defined as `test`

# 17/09/2023

- `pm2`
  - built-in load balancer
  - keep running applications alive indefinitely
  - using `pm2` inside `docker`:
    - not necessary

# 19/09/2023

- hasura
  - remember the hasura geometry query, e.g. `_st_within`
- Docker
  - CMD: will eacute when a container starts
  - attached vs detached
    - attached: keep listing to the port
      - coerk attach CONTAINER to attach a running container
  - docker log to check console.log
  - interactive mode
    - `-it`
  - docker run --rm: automatically remove a stopped container
  - docker inspect CONTAINER
  - docker cp sourcePath desPath
    - copy/export files to/from container
    - use case will be copy logs from container

# 23/09/2023

- MSSQL
  - index: when create index, need to consider the nullable column and should nullable be included in the index.

# 26/09/2023

- MongoDB
  - display in `json` but store in `bson`
  - MongoDB shell
    - can be used as `JS`
    - **Network Access** to control which IP address can access the data
