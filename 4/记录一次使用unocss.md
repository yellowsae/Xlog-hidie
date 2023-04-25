安装 ： `pnpm add  unocss -D`


在 main 中 引入 ：  `import 'virtual:uno.css'`


在 vite 中配置  unocss 

```ts
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import vueJsx from '@vitejs/plugin-vue-jsx'
import UnoCss from 'unocss/vite'
// https://vitejs.dev/config/
export default defineConfig({
  plugins: [UnoCss(), vue(), vueJsx()],
})
```


配置 uno.config.ts
```ts
// uno.config.ts
import {
  defineConfig, presetAttributify, presetIcons,
  presetTypography, presetUno, transformerAttributifyJsx,
} from 'unocss'
export default defineConfig({
  theme: {
  },
  shortcuts: {
    // 这里可以放全局公共样式
    'h-btn': 'h-48px w-100% bg-#5C33BE b-none text-white rounded-8px',
  },
  safelist: [],
  presets: [
    presetUno(),
    presetAttributify(),
    presetIcons({
      extraProperties: { 'display': 'inline-block', 'vertical-align': 'middle' },
    }),
    presetTypography(),
  ],
  transformers: [
    transformerAttributifyJsx(),
  ],
})
```

在 src 下 创建 shims.d.ts  ,  对 TS 未识别的 unocss 属性进行声明  ， 如果在写 unocss 的时候，属性报错就需要在这里添加相应属性的类型


```ts
import * as Vue from 'vue';
declare module 'vue/types/vue' {
  interface HTMLAttributes<T> extends AriaAttributes, DOMAttributes<T> {
    flex?: boolean
    relative?: boolean
    text?: string
    grid?: boolean
    before?: string
    after?: string
    shadow?: boolean
    w?: string
    h?: string
    bg?: string
    rounded?: string
    fixed?: boolean
    b?: string
    z?: string
    block?: boolean
    'focus:shadow'?: boolean
  }
  interface SVGProps<T> extends SVGAttributes<T>, ClassAttributes<T> {
    w?: string
    h?: string
  }
}
```