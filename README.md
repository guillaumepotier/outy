## Outy

[![npm version](https://badge.fury.io/js/outy.svg)](https://badge.fury.io/js/outy)

A simple way to listen for events outside of elements. Inspired by [outside-click](https://github.com/Aloompa/outside-click).

## Install

`yarn add outy`

`npm install outy --save`

```html
<script src="https://unpkg.com/outy/index.js"></script>
(UMD library exposed as `outy`)
```

### Usage
```js
const overlay = document.getElementById('#overlay')
const outsideTap = outy(overlay, ['click', 'touchend'], handleOutsideTap)

function handleOutsideTap() {
  // maybe close an overlay?
}

// cleanup later
outsideTap.remove()
```

### Usage with React
```js
import outy from 'outy'

class MyComponent extends React.Component {
  componentDidMount() {
    const elements = [this.box1, this.box2]
    const types = ['click', 'touchstart']
    const eventHandler = this.handleOutsideTap.bind(this)
    this.outsideClick = outy(elements, types, eventHandler)
  }

  componentWillUnmount() {
    this.outsideClick.remove()
  }

  handleOutsideTap() {
    // close another overlay?
  }

  render() {
    return (
      <div>
        <div ref={c => (this.box1 = c)}>
          Box 1
        </div>
        <div ref={c => (this.box2 = c)}>
          Box 2
        </div>
      </div>
    )
  }
}
```

## API

### outy

Attaches event listeners to document and fires an event whenever any elements outside the provided elements fire.

Returns **remove**

**Parameters**

-   `elements` **[Node|Array](https://developer.mozilla.org/en-US/docs/Web/API/Node)** The element[s] that will reject the event[s]
-   `types` **[String|Array](https://developer.mozilla.org/en-US/docs/Web/Events)** The event type[s] to listen for
-   `eventHandler` **Func** The function that is called when an outside event occurs

### remove

Removes all event listeners.
