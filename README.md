# Devasya website with a product dashboard

What is in this folder
- index.html          the shop (loads products.json)
- intro.mp4           your welcome video
- admin/index.html    the dashboard page (Decap CMS)
- admin/config.yml    dashboard settings  <-- you must edit ONE line in it
- content/products/   one file per product (the dashboard writes these)
- images/products/    your product photos go here (the dashboard uploads them)
- build.js            gathers the product files into products.json on every deploy
- netlify.toml        tells Netlify how to build the site

ONE-TIME SETUP (about 30 minutes)

1. GitHub
   - Create a free account at github.com and a new repository, for example "devasyajewellery" (private is fine).
   - Choose "uploading an existing file", drag in EVERYTHING from this folder (keep the folders), and press Commit.

2. Netlify
   - In Netlify open your site, then Site configuration > Build & deploy > Continuous deployment > Link repository, and choose the GitHub repository.
   - If you do not see that option, choose Add new project > Import an existing project instead, pick the same repository, and then move your domain to the new site under Domain management.
   - Build command: node build.js     Publish directory: .   (netlify.toml already says this)

3. Log-in for the dashboard (GitHub OAuth app)
   - GitHub > your profile picture > Settings > Developer settings > OAuth Apps > New OAuth App.
   - Application name: Devasya CMS
   - Homepage URL: your Netlify address, for example https://your-site.netlify.app
   - Authorization callback URL: https://api.netlify.com/auth/done
   - Press Register, then Generate a new client secret. Keep that page open.
   - In Netlify: Site configuration > Access control (Access & security) > OAuth > Authentication providers > Install provider > GitHub.
   - Paste the Client ID and the Client secret and press Install.

4. Tell the dashboard where your repository is
   - In GitHub open admin/config.yml, press the pencil icon, and change
       repo: YOUR-GITHUB-USERNAME/YOUR-REPO-NAME
     to your real name, for example  repo: rajesh123/devasyajewellery
   - Commit the change. Netlify redeploys by itself.

EVERY DAY: adding a product
1. Open https://www.devasyajewellery.com/admin/  and press Login with GitHub.
2. Products > New Product.
3. Fill in the name, collection and price. Upload the main photo (and more photos if you like). Add the description and "Suitable for".
4. Press Publish (top right). Wait about a minute. The product is live.
To change a price, mark something sold out, or remove a product, open it in the same list.

PHOTO TIPS
- Upright photos, about 4:5 shape, on a plain background look best.
- Netlify makes them small automatically, but every upload is stored in GitHub, so keep each photo under about 1.5 MB.

IF THE LOGIN FAILS
- Open admin/config.yml and remove the # in front of "site_domain:", then put your Netlify address there.
- Make sure the GitHub account you log in with owns the repository (or is a collaborator).
