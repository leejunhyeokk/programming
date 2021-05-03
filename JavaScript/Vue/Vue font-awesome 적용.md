# Vue font-awesome 적용

### 설치

```javascript
$ npm i --save @fortawesome/fontawesome-svg-core
$ npm i --save @fortawesome/free-solid-svg-icons
```



### main.js에 해당 내용을 추가

```javascript
// fontawesome
import { library } from '@fortawesome/fontawesome-svg-core'
import { fas } from '@fortawesome/free-solid-svg-icons'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'

library.add(fas);
Vue.component('font-awesome-icon', FontAwesomeIcon);
```



### 원하는 vue 파일

```javascript
<font-awesome-icon :icon="['fas', ['원하는 아이콘']]"/>
```

