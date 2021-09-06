# MinifyImages Web Application

> Simple frontend browser application to bulk compress images either through
> the browser or using a backend server.
>
> Built with Preact + TailwindCSS

The application was built with Preact which an alternative to React. The end
result is a smaller size application while providing the same DX as a React
project.

The project was mainly inspired from the Squoosh project. I find the idea
of compiling existing C/Rust libraries into WASM format so that it can be used
on the browser extremely interesting as it opens up a lot of possibilities -
which made want to try out on my own.

> **NOTE:** Webpack 4 does not seem to work well with web workers and web
> assembly.  There seem to be multiple issues with it.  Trying to write the
> worker file in Typescript also makes it worse as there seem to be some
> bundling issue.
>
> As of the time of writing, Firefox still does not support module workers
> which means that ES6 import statements would not work. The modules need to be
> inlined/bundled with the worker file for it to work on FF and this usually
> means dealing with bundler and writing custom configs.

## Setup
Follow the following commands to run the development server:
```sh
git clone https://github.com/leo-dh/minifyimages-webapp
cd minifyimages-preact
npm i # or yarn
npm run dev # or yarn dev
```


## Credits

- Icons were obtained from various places, mainly HeroIcons and Ant Design.
- Codecs were edited from the [Squoosh](https://github.com/GoogleChromeLabs/squoosh) project.

## Issues

- There are currently some edge cases where the final file size might end up larger than
  the initial size. This happens due to the additional overhead from
  converting from `ImageData` to `Blob` using JavaScript. In such cases, one might
  be better off using the server option.
