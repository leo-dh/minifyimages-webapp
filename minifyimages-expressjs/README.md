# MinifyImages API Server

> Simple API server written in Typescript using Express as the framework of
> choice.

The main purpose of the server is to serve RESTful API requests from the
frontend application. Ultimately, this serves as a backup - in the scenario
where the WASM files fails to load for some unknown reason or if the user's
device is too slow and using a server to perform the compressions is much
faster.


## Functions
The images are compressed using the `imagemin` nodejs library. JPEG files will be processed
using either the `mozjpeg` library (lossy) or the `jpegtran` library (lossless). Likewise,
for PNG files, the libraries used are `pngquant` (lossy) and `optipng` (lossless).

The server uses a worker pool to ensure that the main event loop stays
responsive to new API requests while it compresses the images.

The minified images will remain on the server for an hour before being deleted.

All requests will be logged using a logger middleware. Request logs can be found
in `logs/requests.log` while errors will be in `logs/errors.log`. `logs/activity.log` would
show both requests and errors.

## Endpoints
### `POST` /minify
#### Parameters
##### `quality` (optional)
Level of quality of the compressed image. Valid values: `0 - 100`. If this parameter
is not specified, the server will assume that it is a lossless compression.
#### Response
```json
{
  "initialSize": 0,
  "finalSize": 0,
  "url": "string",
  "filename": "string",
}
```

## Setup
Run the following commands to setup the development server:
```sh
git clone https://github.com/leo-dh/minifyimages-webapp
cd minifyimages-expressjs
npm i # or yarn
npm run start or # yarn start
```

The development server can be accessed using the following address: `http://localhost:5000`.
To run the server on a different port, you can specify the environment variable `PORT`, either
in a `.env` file at the current directory or in the command line.
