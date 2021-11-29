## Reference data

> This feature previously used a bracket (`[]`) to tell where to replace the data, now you need to change it with the double curly brackets (`{{}}`)

You can use this feature if you want to add dynamic data in the input of a block like in the selector or the form value. To get started, you can write `{{ keyword@path }}` in the input of a block. In `keyword` write the source of the data, there are three sources where you can get the data from:

1. `dataColumns`: get data from the data columns.
2. `loopData`: get the iteration data from the [loop data block](https://github.com/Kholid060/automa/wiki/Blocks/_edit#loop-data).
3. `prevBlockData`: get data from the previous block.
4. `globalData`: get the global data that you have defined.
5. `activeTabUrl`: get the currently active tab url.


And `path` is where you write the key of the data and nested key also supported. The syntax is could be different on each of the sources of the data

### Data columns
Because the data of data columns is an array of objects that looks like this
```js
[
  { city: 'london', country: 'england' },
  { city: 'ottawa', country: 'canada' },
  { city: 'jakarta', country: 'Indonesia' },
]
```
To get the first data, you can write `{{ dataColumns@0.city }}` and the output would be `London`. To get the second data write `{{ dataColumns@1.city }}` and so on.

### Loop data
To get the iteration data of the [loop data block](https://github.com/Kholid060/automa/wiki/Blocks/_edit#loop-data), you must write the loop ID first before the `path` for example `{{ loopData@loopID.path }}`.

### Previous block data
Get data from the previous block. Because all blocks are returning data, like a get text block that returns the text that it got from the element. To get the data, write `{{ prevBlockData }}`.
