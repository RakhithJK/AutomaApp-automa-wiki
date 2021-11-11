## Reference data

You can use this feature if you want to add dynamic data to the block. To get started, you can write `{{ keyword@path }}` in the input of a block. In `keyword` write the source of the data, there are three sources where you can get the data from:

1. `dataColumns`: get data from the data columns.
2. `prevBlockData`: get data from the previous block.
3. `loopData`: get data from the loop block.

And `path` is where you write the key of the data. For example, because the structure of data columns looks like this
```js
[
  { city: 'london', country: 'england' },
  { city: 'ottawa', country: 'canada' },
  { city: 'jakarta', country: 'Indonesia' },
]
```
If you want to get the first data, you can write `{{ dataColumns@0.city }}` and the output would be `London`. To get the second data write `{{ dataColumns@1.city }}` and so on.