# vue-confirm-message

Vue message component

#### Installation

```
npm i -D vue-confirm-message
```


#### Example

```
<VueConfirmMessage :title="'Show message box'"
                   :message="'Select Yes or No'"
                   :yes="'Yes'"
                   :no="'No'"
                   :shortcuts="true"
                   @confirm="myMethod(true)"
                   @cancel="myMethod(false)"/>
```

```
import ConfirmMessage from 'vue-confirm-message'
```

```
components: {
  ConfirmMessage
}

methods: {
  myMethod (status) {
    console.log(`Selected ${status ? 'Yes' : 'No'}`)
  }
}
```
