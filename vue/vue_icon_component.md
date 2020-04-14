# 你不知道的 Vue 的图标组件

封装一个图标组件，可以配置某一个图标，可以设置是否旋转，可以追加字体图标。特点简单实用，灵活可配。

## 一个 Vue 的文件

### 共有 class

封装一个图标组件首先从一个 vue 文件开始，其主要的结构就是一个 `i` 标签。最关键的就是这个 class 名的配置。有一个共有的 w-icon 类名负责自定义字体，这个字体就是从字体图标工具中下载的包括自定义字体图标的字体，还包括一些共有的样式。

### 定义字体图标的 class

光有一个共有的类名可不行，不同的字体图标是通过不同的 class 名配置的，我们得需要一个 prop 来设置显示的字体图标，我们把这个 prop 设定为 `type` ，类型为 `String` 。如果不传类型的时候，我们就不显示这个 icon 。

### 设定是否旋转的 class

这里有一个高级功能那就是可配置的旋转动画。我们需要一个 prop 来设置是否需要旋转动画，我们把这个 prop 设定为 `spin` ，类型为 `Boolean` 。如果为 true ，那么我们就让它转起来。

### 设定 class 的前缀参数

w-icon 默认前缀为 `w` ，如果您需要扩展字体图标，或者需要自定义样式，我们为您提供了一个 prop 。专为此事而行，这个 prop 我们设定为 `prefix` ，类型为 `String` ，默认为 `w` 。

### vue 组件源码奉上

```
<template>
  <i
    v-if="type"
    :class="[`${prefix}-font`,`${prefix}-${type}`, {
      'w-spin': !!spin,
    }]"
  ></i>
</template>

<script>
export default {
  name: 'WIcon',
  props: {
    type: String,
    spin: Boolean,
    prefix: {
      type: String,
      default: 'w',
    },
  },
  data() {
    return {};
  },
};
</script>
```

## 一个 SCSS 的文件

我们已经有一个像样的 vue 文件，那么我们还需要让 vue 的 icon 组件美起来的样式文件。这里我们选择的预处理器为 SCSS 。在这个样式文件中，我们需要做三件事⤵️

- 声明字体图标的字体
- 设置共有样式 w-font
- 设置字体图片类型的众多样式，如 w-loading 等
- 设置旋转动画类型 `w-spin`
- 设置旋转动画

### 声明字体图标的字体

这里我们利用 CSS3 的自定义字体的属性来完成这项使命。需要注意的是根据不同浏览器支持的字体后缀来做好适配。

### 设置共有样式 w-font

声明好字体之后，就可以用了。用法和普通设置字体是一样的，名字就用之前咱们设置好的就可以了。除了设置字体之外，我们还需要做一些特殊处理。如居中等。设置 text-rendering 为 optimizeLegibility 。它使得对于某些字体（例如，Microsoft的Calibri，Candara，Constantia和Corbel或DejaVu字体系列），文本中的连字（ff，fi，fl等）小于20px。

### 设置字体图片类型的众多样式

这个就是根据导出的字体图标，在 before 伪元素中设置字体图标的内容即可。如果有共同特点，如 w-loading1 , w-loading2 等，可以实用 sass 中的循环来优化写法。

### 设置旋转动画类型 `w-spin`

这里使用了 CSS3 中的 动画属性 (animation) 。让它执行 loadingCircle 动画，并且无线的匀速执行下去，每次动画时间为 1 秒。

### 设置旋转动画

利用 `@keyframes` 关键字声明一个动画，名为 loadingCircle 。在最开始的时候旋转基点定为图标中心点，并旋转角度为 0 度。在最结束的时候定义旋转基点定为图标中心点，并旋转角度为 1 圈( trun )。

### scss 样式源码奉上

```
$font-name: "iconfont";
$font-version: 1524475512080;
$font-prefix: 'w-';
$font-path: './icon/font/';

@font-face {
  font-family: $font-name;
  src: url('#{$font-path}iconfont.eot?t=#{$font-version}');
  src:
    url('#{$font-path}iconfont.eot?t=#{$font-version}#iefix') format('embedded-opentype'),
    url("#{$font-path}iconfont.woff?t=#{$font-version}") format("woff"),
    url('#{$font-path}iconfont.ttf?t=#{$font-version}') format('truetype'),
    url('#{$font-path}iconfont.svg?t=#{$font-version}#iconfont') format('svg');
}

.#{$font-prefix}font {
  font-family: $font-name !important;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: inline-block;
  font-style: normal;
  vertical-align: baseline;
  text-align: center;
  text-transform: none;
  line-height: 1;
  text-rendering: optimizeLegibility;
}

.#{$font-prefix}back::before { content: "\e934"; }

.#{$font-prefix}forward::before { content: "\e94d"; }

$font-list: "\e66a" "\e668" "\e669" "\e667";
// 循环 $font-list 并设置类名
// 其中 index 方法是获取索引
@each $font-item in $font-list {
  .#{$font-prefix}loading#{index($font-list, $font-item)}::before {
    content: $font-item;
  }
}

.#{$font-prefix}spin::before {
  display: inline-block;
  animation: loadingCircle 1s infinite linear;
}

@keyframes loadingCircle {
  0% {
    transform-origin: 50% 50%;
    transform: rotate(0deg);
  }

  to {
    transform-origin: 50% 50%;
    transform: rotate(1turn);
  }
}
```

## 注册 w-icon 组件

要注册一个组件，必须这个组件中拥有 `install` 方法。有了这个方法，在其回调中的 Vue 参数中调用 `component` 方法，即可。方法如下⤵️

```
import WIcon from './Icon';

WIcon.install = (Vue) => {
  Vue.component(WIcon.name, WIcon);
};

export default WIcon;
```

## 写一个图标组件的单元测试

单元测试一个图标组件，我们需要测试其属性是否真正用到了，是否与预期的一样。我们需要测试其快照的 UI 是否是我们想要的 UI 。我们不传 type 属性不显示的特殊处理是否真的生效。我们自定义前缀是否真的自定义了。

我们在一开始需要实例化组件，我们可以用 `vue-test-utils` 中的 `mount` 方法。当 DOM 更新之后， `this` 绑定到当前实例上之后( $nextTick ) 做一些事情。

具体测试代码⤵️

```
import { mount } from 'vue-test-utils';
import Icon from './Icon';

describe('Icon.vue', () => {
  let wrapper = null;
  let wrapperNo = null;
  let wrapperPrefix = null;
  let wrapperSpin = null;

  // 实例化
  beforeEach(() => {
    // 传入 loading1 ，然后去检测实例化之后 type 是否是 loading1 。
    wrapper = mount(Icon, {
      propsData: {
        type: 'loading1',
      },
    });
    // 不向其传任何参数，去检测针对 type 为空不显示的特殊处理是否生效。
    wrapperNo = mount(Icon);
    // 传前缀 test ，测试实例化之后的前缀是否完全改变
    wrapperPrefix = mount(Icon, {
      propsData: {
        type: 'loading1',
        prefix: 'test',
      },
    });
    // 实例化之后图标是否拥有旋转动画
    wrapperSpin = mount(Icon, {
      propsData: {
        type: 'loading1',
        spin: true,
      },
    });
  });

  it('验证 prop 值是否正确', (done) => {
    wrapper.vm.$nextTick(() => {
      try {
        expect(wrapper.props().type).toBe('loading1');
        done();
      } catch (err) {
        done.fail(err);
      }
    });
  });

  it('验证 class 值是否正确', (done) => {
    wrapper.vm.$nextTick(() => {
      try {
        expect(wrapper.is('i')).toBe(true);
        expect(wrapper.classes().toString()).toBe('w-font,w-loading1');
        done();
      } catch (err) {
        done.fail(err);
      }
    });
  });

  it('验证 prop 为空不显示', (done) => {
    wrapperNo.vm.$nextTick(() => {
      try {
        expect(wrapperNo.is('i')).toBe(false);
        done();
      } catch (err) {
        done.fail(err);
      }
    });
  });

  it('验证 自定义前缀 prefix', (done) => {
    wrapperPrefix.vm.$nextTick(() => {
      try {
        expect(wrapperPrefix.is('i')).toBe(true);
        expect(wrapperPrefix.classes().toString()).toBe('test-font,test-loading1');
        done();
      } catch (err) {
        done.fail(err);
      }
    });
  });

  it('验证 spin 字段转动', (done) => {
    wrapperSpin.vm.$nextTick(() => {
      try {
        expect(wrapperSpin.is('i')).toBe(true);
        expect(wrapperSpin.classes().toString()).toBe('w-font,w-loading1,w-spin');
        done();
      } catch (err) {
        done.fail(err);
      }
    });
  });

  it('检测快照是否一样。', (done) => {
    wrapper.vm.$nextTick(() => {
      try {
        // 检测 UI 是否改变
        expect(wrapper.text()).toMatchSnapshot();
        done();
      } catch (err) {
        done.fail(err);
      }
    });
  });
});
```

## 源码

更完整的源码，请移步 [w-icon](https://github.com/fe6/water/tree/master/water/icon) 。
