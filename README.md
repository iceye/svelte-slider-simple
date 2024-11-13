# svelte-slider-simple

Simple svelte range slider component using the code before the fork. [demo](https://svelte.dev/repl/e93d43c42b434e3aa3e2a5815f805c75?version=3.22.3)
This repo has a simpler version to bind value directly to a variable, unfortunately range slider cannot be used in this configuration.

## Install

Install with npm or yarn:

```bash
npm i -D @iceye/svelte-slider-simple
```

Then import `Slider` component to your Svelte app.

```js
import Slider from '@iceye/svelte-slider-simple';
```

## Usage

### Simple usage
```html
<Slider bind:value >
```

### Range input
```html
<Slider bind:value />
```

### Min, max and step
```html
<Slider min="-50" max="50" step="10" bind:value />
```

You can `bind`  value, slider will change according to props change

### Slots

Simple slot only
```html
<Slider bind:value>
  <span style="font-size: 20px;">&#128079;</span>
</Slider>
```


## Props

|Name|Type|Default|Description|
|---|---|---|---|
|value|number|`50`||
|min|number|`0`||
|max|number|`100`||
|step|number|`1`||
|name|Array [string, string]|empty array|Provide names to inputs if you want use slider in form input|

## Slots

- `default` - customizes both thumbs if `left` slot isn't provided
- `left` - provide to customize left thumb


## Events

- `input` - event fires when the value changes within thumb drag

## Style

```css
:root {
  --track-bg: #ebebeb;
  --progress-bg: #8abdff;
  --thumb-bg: #5784fd;
}
```

set `--thumb-bg` to `transparent` if you use custom thumb
```css
:root {
  --thumb-bg: transparent;
}
```

## License

MIT &copy; iceye