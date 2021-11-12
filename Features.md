## Reference data

> This feature previously used a bracket (`[]`) to tell where to replace the data, now you need to change it with the double curly brackets (`{{}}`)

You can use this feature if you want to add dynamic data in the input of a block like in the selector or the form value. To get started, you can write `{{ keyword@path }}` in the input of a block. In `keyword` write the source of the data, there are three sources where you can get the data from:

1. `dataColumns`: get data from the data columns.
2. `prevBlockData`: get data from the previous block.
3. `loopData`: get data from the [loop data block](https://github.com/Kholid060/automa/wiki/Blocks/_edit#loop-data) block.

And `path` is where you write the key of the data and it's optional. It depends on the structure of the data if the data is an array of objects like the data columns for example that looks like this
```js
[
  { city: 'london', country: 'england' },
  { city: 'ottawa', country: 'canada' },
  { city: 'jakarta', country: 'Indonesia' },
]
```
To get the first data, you can write `{{ dataColumns@0.city }}` and the output would be `London`. To get the second data write `{{ dataColumns@1.city }}` and so on. If the data is nested like this
```js
[
  {
    key: {
      deepKey: {
        deeperKey: 'deeper key value',
      },
      first: 'foo',
      last: 'bar',
    },
  }
]
```
to get the value of `deeperKey` you can write `{{ dataColumns@0.key.deepKey.deeperKey }}`.