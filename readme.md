# Installation

![screenshot](./screenshot.png)


```
yarn add vue-bootsrtap-time-picker 
```
or
```
npm i vue-bootstrap-time-picker --save-dev
```

# Usage
Register the component in your vue files as :

```javascript
import TimePicker from 'vue-bootstrap-time-picker';

export default {
    components: {
        TimePicker
    },

    data() {
        return {
            time: ''
        }
    }
}
```

```html
<form>
    <time-picker v-model="time" />
</form>
```
