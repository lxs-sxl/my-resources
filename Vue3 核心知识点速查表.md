# 一、应用创建与项目结构

内容	说明
创建应用	import { createApp } from 'vue'
入口文件	main.js，调用 createApp(App).mount('#app')
根组件	App.vue，单文件组件格式
构建工具	Vite（推荐），配置文件 vite.config.js

# 二、组合式 API (Composition API)

内容	说明
ref	用于基本类型或对象的响应式数据，需 .value 访问
reactive	用于对象类型的响应式数据
computed	计算属性，具有缓存，依赖响应式数据
watch	监听响应式数据变化，支持 immediate 和 deep
watchEffect	自动追踪其内部响应式依赖
setup	组合式 API 的入口函数，<script setup> 语法糖
生命周期钩子	onMounted, onUpdated, onUnmounted 等，需导入使用

# 三、模板语法与指令

指令	说明
{{ }}	插值表达式
v-model	双向绑定，语法糖
v-if / v-show	条件渲染
v-for	列表渲染，建议配合 :key
v-bind (:)	动态绑定属性
v-on (@)	事件绑定
v-slot (#)	插槽语法

# 四、组件通信

通信方式	说明
Props	父组件向子组件传递数据
Emits	子组件向父组件传递数据
provide / inject	跨层级传递数据
$refs	获取 DOM 或子组件实例
Pinia	全局状态管理，替代 Vuex

# 五、响应式系统

内容	说明
实现方式	Vue3 使用 Proxy 实现响应式
ref 与 reactive	ref 用于基本类型，reactive 用于对象
computed	基于响应式数据派生新值，有缓存
watch	监听响应式数据变化
$nextTick	DOM 更新后执行回调，保证获取最新 DOM

# 六、生命周期钩子

Vue2 钩子	Vue3 对应钩子	说明
beforeCreate	无	组合式 API 中无需
created	无	组合式 API 中无需
beforeMount	onBeforeMount	组件挂载前
mounted	onMounted	组件挂载后
beforeUpdate	onBeforeUpdate	组件更新前
updated	onUpdated	组件更新后
beforeUnmount	onBeforeUnmount	组件卸载前
unmounted	onUnmounted	组件卸载后

# 七、新增特性与内置组件

特性	说明
Fragment	支持多个根节点
Teleport	将组件渲染到任意 DOM 位置
Suspense	处理异步组件加载状态
v-model 语法糖	<input v-model="msg"> 等价于 <input :value="msg" @input="msg = $event.target.value">

# 八、性能优化

优化点	说明
Proxy 响应式	更好支持对象属性新增/删除
静态提升	编译时优化，跳过静态节点
Tree-shaking	按需打包，减少体积
key 值	帮助 Vue 复用、移动或销毁节点，避免使用 index 作 key

# 九、常用函数与工具

函数	说明
createApp	创建 Vue 应用实例
ref	创建响应式数据（基本类型）
reactive	创建响应式对象
computed	创建计算属性
watch / watchEffect	数据监听
onMounted / onUnmounted 等	生命周期钩子
defineProps / defineEmits	<script setup> 中定义 Props 和 Emits

# 十、项目结构关键文件

文件	说明
main.js	应用入口
App.vue	根组件
vite.config.js	Vite 配置文件
index.html	单页入口，提供 id="app" 挂载点
package.json	项目依赖和脚本配置