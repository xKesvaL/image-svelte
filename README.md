# Svelte Optimized Images 🪄📈

[![Version](https://img.shields.io/npm/v/@kesval/image-svelte?style=for-the-badge)](https://www.npmjs.com/package/@kesval/image-svelte) [![Issues](https://img.shields.io/github/issues/xKesvaL/image-svelte?style=for-the-badge)](https://github.com/xKesvaL/image-svelte/issues) [![License](https://img.shields.io/github/license/xKesvaL/image-svelte?style=for-the-badge)](https://github.com/xKesvaL/image-svelte/blob/main/LICENSE)

- [Svelte Optimized Images 🪄📈](#svelte-optimized-images-)
  - [Usage](#usage)
    - [Important](#important)
    - [Component Props](#component-props)
      - [Styling](#styling)
    - [Image Package Customization](#image-package-customization)
    - [Vercel](#vercel)
    - [Dev Mode](#dev-mode)
  - [Create your own component](#create-your-own-component)
  - [Svelte Starter](#svelte-starter)

## Usage

To use this package it is very important to have installed the following packages: `@kesval/image` and to have these scripts in your `package.json`:

```json
{
  "scripts": {
    "optimize-images": "image-opti --source ./build/<sourceFolder> --target ./build/<targetFolder>",
    "postbuild": "npm run optimize-images"
  }
}
```

You can replace `<sourceFolder>` and `<targetFolder>` with the folders where your images are usually in your `static` folder.

For example, if you have your images in `static/images` you can replace `<sourceFolder>` with `images` and `<targetFolder>` with `images-opti`.

### Important

It is mandatory that the script `optimize-images` is executed after the build script, or otherwise the build script will overwrite the optimized images.

### Component Props

The component accepts the following props (with typesafety):

- `src: string`
- `alt: string`
- `formats?: string[]` (default: `['webp', 'png', 'jpg']`)
- `widths?: string[]` (default: `null` - base width)
- `figcaption?: string` (default: `null`)
- `loading?: 'lazy' | 'eager'` (default: `lazy`)
- `figureClasses?: string` (default: `''`)
- `imgClasses?: string` (default: `''`)

#### Styling

You can add classes to the component using the figureClasses (which go on the `figure` tag) and imageClasses (which go on the `img` tag inside) props:

```svelte
<script>
  import Image from '@kesval/image-svelte'
</script>

<Image figureClasses="class1 class2" imgClasses="class3 class4" >
```

### Image Package Customization

The default behavior of the package is to optimize all `jpg`, `jpeg` and `png` images to `webp` without changing their width.

For further customization of the script you can add -h to the args or you can check the [documentation](https://github.com/kesval/image).

### Vercel

If you are deploying your app on vercel, you just have to replace your source and destination folders like so:

```json
{
  "scripts": {
    "optimize-images": "image-opti --source .vercel/output/static/<sourceFolder> --target .vercel/output/static/<targetFolder>",
    "postbuild": "npm run optimize-images"
  }
}
```

### Dev Mode

Just note that in dev mode, the raw images will be served, not the optimized ones. This is because the images are optimized at build time.

If you need to have an idea of how big the images will be, you can just run the script: `npm run optimize-images -- -v` (enables verbose) and check the size of the images in the command line or in the target folder.

## Create your own component

By default, the component simply renders an `img` tag with the `src` attribute pointing to the optimized image. If you want to customize this behavior, you can create your own component. For example, you can show an error image if the image fails to load:

```svelte
<script>
  import Image from '@kesval/image-svelte'
</script>

<Image let:error let:alt let:src>
  {#if error}
    placeholder error image
  {:else}
    <img src={src} alt={alt} srcset={srcSet} />
  {/if
</Image>
```

The component will pass the following props to the parent:
`src`, `srcSet`, `alt`, `error`, `loading`, `figcaption`

## Svelte Starter

This package is included in my [Svelte Starter](
  https://github.com/xKesvaL/starter-svelte
) template. Check it out!
