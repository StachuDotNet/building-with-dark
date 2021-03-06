## Hosting Static Assets

Dark supports hosting your static assets.

Our static assets service is designed to be simple, easy to understand, as well as composable and configurable. As such, a static assets deploys uploads your assets to our cloud CDN, and we provide powerful tools in Dark to serve and configure them.

A GitHub Action to automate this process is available.

### uploading/deploy static assets
- go to https://Dark-cli.storage.googleapis.com/index.html and download the appropriate binary
- `chmod +x Dark-cli-linux` // to make it executable
- confirm it works with `./Dark-cli-linux -- help`
- configure your client
	- at the moment, our CDN does not support the use of absolute URLs is the generated files. For example, if your CSS file links an image at /static/myimage.png, that file will not load. You need to use relative URLs instead, in this case ./myImage.png
	- Your index.html likely loads other assets, such as app.css or app.js. For speed, you will load these directly from the Dark CDN, not via your Dark handler. As such, we'll need to make some edits to your assets to ensure they're always pointing at the CDN for other assets.
	- During the deployment of the assets, our backend replaces the string DARK_STATIC_ASSETS_BASE_URL in all of your assets with the actual URL of this deployment
	- when not using a framework, prefix asset paths with Dark's magic string, for example
	- <img src="DARK_STATIC_ASSETS_BASE_URL/logo.svg" />
	- In react, when compiing your react application, you can use PUBLIC_URI:
	- PUBLIC_URL=DARK_STATIC_ASSETS_BASE_URL npm run build
- deploy
	- To deploy, select the directory you want to upload. In this case, we'll use React's default directory `build`
	- Run
		- `./Dark-cli-linux --canvas myusername-mycanvas --password '' --?`
	- on success, we'll show you the deploy hash, a URL, and a long URL. THese are where your static assets now live! You can see your static assets in the Routing table in your canvas
- Set up your app to Load your Assets
	- if your spa framework generates an index.html, or you write one yourself, you can load that for the / route in Dark
	- Add a handler for / to load your index.html page using StaticAssets::serveLatest "index.html"
	- If you're using client-side routing, you can also add a handler serving index.html for /:rest which will be a catch-all handler for any URL (besides /) that doesn't have another handler defined for it. This will allow your users to load your assets from any of your app's URLs

### using static assets
- StaticAssets::
	- ::baseUrlFor
	- ::baseUrlForLatest
	- ::fetchBytes
	- ::fetchLatestBytes
	- ::fetchLatest 
	- ::fetch <deployHash:String> <file:String> -> String
	- Returns the contntes of a file for the current canvas and the given deployHash
	- ::serveLatest
	- ::serve
	- ::urlFor <deployHash:String> <file:String> -> string
		- returns a URL to a file for the current canvas and given deployHash
		- ::urlFor "o6vs1aqcbs" "foo.html" -> "https://ismith-wlbtgta563t8/o6vs1aqcbx/foo.html"
	- StaticAssets::urlForLatest

### implementing a fallback in the case of a 404
if you're looking to serve a fallback asset, you can use a match stateemnt:

```
let resp = StaticAssets::serveLatest fileName
match resp
  Ok resp -> resp
  Error resp -> "This is an error"
  Default -> StaticAssets::serveLatest "index.html"
```

### Unorganized:
- uploading
- UI
- usage
- future: deletions
- show demo
- better URL for getting the ...upload download
-