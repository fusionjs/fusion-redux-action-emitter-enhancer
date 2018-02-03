# fusion-redux-action-emitter-enhancer

[![Build status](https://badge.buildkite.com/1864b671ca8edc1b7a6f8470ae320c6163268c23c4085ee82a.svg?branch=master)](https://buildkite.com/uberopensource/fusion-redux-action-emitter-enhancer)

Redux store enhancer that emits actions via an injected event emitter.

---

### Example

```js
// src/main.js
import UniversalEvents, {UniversalEventsToken} from 'fusion-plugin-universal-events';
import {FetchToken} from 'fusion-tokens';
import Redux, {ReduxToken, ReducerToken, EnhancerToken} from 'fusion-plugin-react-redux';
import fetch from 'unfetch';
import ReduxActionEmitterEnhancer from 'fusion-plugin-redux-action-emitter-enhancer';
import reducer from './reducers/root.js'

export default function start() {
  const app = new App(root);

  app.register(UniversalEventsToken, UniversalEvents, {fetch});
  __BROWSER__ && app.register(FetchToken, fetch);

  app.register(ReduxToken, Redux);
  app.register(ReducerToken, reducer);
  app.register(EnhancerToken, ReduxActionEmitterEnhancer);

  return app;
}

// src/reducers/root.js
export default (state, action) => {
  // reducer goes here
}
```

---

### API

#### Dependency registration

```js
import UniversalEvents, {UniversalEventsToken} from 'fusion-plugin-universal-events';

app.register(UniversalEventsToken, UniversalEvents);
```

#### Required dependencies

Name | Type | Description
-|-|-
`UniversalEventsToken` | `UniversalEvents` | An event emitter plugin, such as the one provided by [`fusion-plugin-universal-events`](https://github.com/fusionjs/fusion-plugin-universal-events).

#### Instance API

To consume action events, add an event listener for the following emitted events:

- `redux-action-emitter:action`

---
