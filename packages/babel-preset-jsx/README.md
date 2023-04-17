# fork from https://github.com/vuejs/jsx-vue2

解决在 vue 中使用 jsx 时，无法使用原生 slot 的问题.
由于 vue 的 slot 与原生 slot 解析存在冲突，因此对于 quark 使用的原生 slot，使用时请加上前缀 `quark-slot`.

```tsx
import { Component, Vue } from "vue-property-decorator";
import 'quarkd/lib/dialog'

@Component({})
export default class Home extends Vue {
  render() {
    return (
      <div>
        <h1>Hello world</h1>
        <quark-dialog content="testts" open>
          <div quark-slot="title" >自定义标题</div>
        </quark-dialog>
      </div>
    )
  }
}
```

## @quarkd/babel-preset-jsx

Configurable preset for Vue JSX plugins.

### Babel Compatibility Notes

- This repo is only compatible with Babel 7.x, for 6.x please use [vuejs/babel-plugin-transform-vue-jsx](https://github.com/vuejs/babel-plugin-transform-vue-jsx)

### Usage

Install the dependencies:

```sh
# for yarn:
yarn add @quarkd/babel-preset-jsx @vue/babel-helper-vue-jsx-merge-props
# for npm:
npm install @quarkd/babel-preset-jsx @vue/babel-helper-vue-jsx-merge-props --save
```

In your `babel.config.js`:

```js
module.exports = {
  presets: ['@quarkd/babel-preset-jsx'],
}
```

You can toggle specific features, by default all features (except `compositionAPI`) are enabled, e.g.:

```js
module.exports = {
  presets: [
    [
      '@quarkd/babel-preset-jsx',
      {
        vModel: false,
        compositionAPI: true,
      },
    ],
  ],
}
```

Options are:

- `compositionAPI` - Enables [@vue/babel-sugar-composition-api-inject-h](../babel-sugar-composition-api-inject-h) and [@vue/babel-sugar-composition-api-render-instance](../babel-sugar-composition-api-render-instance), support returning render function in `setup`.
  - The default value is `false`;
  - When set to `'auto'` (or `true`), it will detect the Vue version in the project. If it's >= 2.7, it will import the composition utilities from `vue`, otherwise from `@vue/composition-api`;
  - When set to `'native'` (or `'naruto'`), it will always import the composition utilities from `vue`
  - When set to `plugin`, it will always import the composition utilities from `@vue/composition-api`, but it will redirect to `'vue'` itself when the vue version is `2.7.x`
  - When set to `vue-demi`, it will always import the composition utilities from `vue-demi`
  - When set to an object like `{ importSource: string; }`, it will always import the composition utilities from the importSource you set
- `functional` [@vue/babel-sugar-functional-vue](../babel-sugar-functional-vue/README.md) - Functional components syntactic sugar
- `injectH` [@vue/babel-sugar-inject-h](../babel-sugar-inject-h/README.md) - Automatic `h` injection syntactic sugar
- `vModel` [@vue/babel-sugar-v-model](../babel-sugar-v-model/README.md) - `vModel` syntactic sugar
- `vOn` [@vue/babel-sugar-v-on](../babel-sugar-v-on/README.md) - `vOn` syntactic sugar
