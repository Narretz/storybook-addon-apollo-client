# Storybook Addon Apollo Client

Use Apollo Client in your Storybook stories.

## Versions

- If you're using Apollo Client 2.x and Storybook 5.x use version 1.x
- If you're using Apollo Client 2.x and Storybook 6.x use version 2.x
- If you're using Apollo Client 3.x and Storybook 6.x use version 3.x

## Install

**yarn**
```
yarn add --dev storybook-addon-apollo-client
```

**npm**

```
npm install -D storybook-addon-apollo-client
```

## As a decorator in a story

```jsx
import { withApolloClient } from 'storybook-addon-apollo-client';
import MyComponentThatHasAQuery, {
  MyQuery,
} from '../component-that-has-a-query';

export default {
  title: 'My Story',
  decorators: [withApolloClient],
};

export const example = () => <MyComponentThatHasAQuery />;

example.story = {
  parameters: {
    apolloClient: {
      mocks: [
        { request: { query: MyQuery }, result: { data: { viewer: null } } },
      ],
    },
  },
};
```

## Usage in `preview.js`

```js
import { withApolloClient } from 'storybook-addon-apollo-client';
import { addDecorator } from '@storybook/react';
import { InMemoryCache } from 'apollo-cache-inmemory';

const cache = new InMemoryCache();

addDecorator(
  withApolloClient({
    cache,
    ...// take a look at all the options in https://www.apollographql.com/docs/react/development-testing/testing
    // everything that is used in `storybook-addon-apollo-client` is a 1 to 1 mapping of MockedProvider
  })
);
```

if you setup `withApolloClient` in preview, it will not need to be added to the `decorators` key in each story, consider doing this if you have a lot of stories that depend on Apollo.

Read more about the options available for MockedProvider at https://www.apollographql.com/docs/react/development-testing/testing

## Example App

To see real world usage of how to use this addon, check out the example app:

https://github.com/lifeiscontent/realworld
