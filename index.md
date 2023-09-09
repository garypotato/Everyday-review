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
