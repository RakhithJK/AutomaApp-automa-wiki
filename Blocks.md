## Trigger
This is block is the starting point where the workflow will start executing, you can configure how the workflow should be triggered using this block.
### Manually
Manually trigger the workflow by clicking the play (▶️) button.
### Interval
Execute the workflow in intervals, you can define the interval and the delay before executing the workflow in provided input.
### On a specific date
Execute the workflow on a specific date and time.
### On a specific day
Execute the workflow on a specific day and time, like ff you want to execute a workflow every day or every Sunday and Tuesday at 9 AM, you can use this option.
### When visiting a website
The workflow will automatically be executed when you're visiting a website that matches the URL or the [ReGex](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions) that you inputted. And when you check the `Use regex` checkbox, the value you inputted will be treated as a [ReGex](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Regular_Expressions).

You can directly connect the trigger block with the block in the web interaction category when you use this option and the workflow will be executed on the website that you're in.

### Keyboard shortcut
Execute the workflow using a keyboard shortcut. You can specify the keyboard shortcut by clicking the record (⏺️) button and pressing the key that you want to use.

The keyboard shortcut only works when you're on a website. And by default, the shortcut doesn't work when the cursor is on an input element, so to prevent this behavior click the "Active while in input" checkbox.

## Javascript code
When automa doesn't have a block to handle a certain situation in the web page, like comparing two values of DOM for instance. You can insert your javascript code logic with this block, the code will execute on the web page when it is fully loaded.

Here is the example of code when you want to compare two values of DOM
```js
const input1 = document.querySelector('.first-input')
const input2 = document.querySelector('.second-input')

if (input1.value === input2.value) {
  // Do something
} else {
  // Do something
}

automaNextBlock();
```
At the end of the code, you see `automaNextBlock`. This function is for telling the workflow to execute the next block. 

There are two functions you can execute inside the javascript code.

### `automaNextBlock(data)`
To tell the workflow to execute the next block. This function accepts one parameter which you can use to save data into the workflow data columns, the parameter must be an `object` or an `array of objects`. You must use the column that you added as a key for the object, for example when you have added the `text` column the code should look like.
```js
// object
automaNextBlock({ text: 'lorem ipsum' })

// array of objects
automaNextBlock([{ text: 'lorem ipsum' }, { text: 'lorem ipsum 2' }])
```
### `automaResetTimeout()`
Because this block has an execution timeout, it will automatically execute the next block when the timer expires. So to reset this timer, you can call this function.

### `automaRefData(keyword, path)`
Use this function to [reference data](https://github.com/Kholid060/automa/wiki/Features#reference-data).

## Google sheets
Get data from [Google Sheets](https://www.google.com/sheets/about/). And make sure you share the spreadsheet that you want to use as a public, to do that you can click the Share button and copy the link like the image below

![Google sheets URL](https://res.cloudinary.com/chat-story/image/upload/v1641014063/automa/Screenshot_2022-01-01_131346_ityxor.png)

### Spreadsheet Id
The Spreadsheet Id contains letters, numbers, hyphens, or underscores. And you can find it in the Google Sheets URL
`
https://docs.google.com/spreadsheets/d/SpreadsheetID/edit?usp=sharing
`

![image](https://res.cloudinary.com/chat-story/image/upload/v1641768594/automa/chrome_OuX2wQzOe4_lyd8tv.png)

### Range
You can define the range of the cells that you want to get or update from the spreadsheet, you can input [A1 Notation](https://developers.google.com/sheets/api/guides/concepts#expandable-1) syntax like `Sheet1!A1:B2` or [R1C1 Notation](https://developers.google.com/sheets/api/guides/concepts#expandable-2) syntax like `Sheet1!R1C1:R2C2` in here.

### Reference key
Use the key that you write here whenever you want to [reference data](https://github.com/Kholid060/automa/wiki/Features#reference-data) of the google sheets. For example, if you input `list` as the key and you want to use them as the value at the **Forms** block, you can input `{{ googleSheets@list.path }}`.

### Update spreadsheet cells
To be able to update the cells of the spreadsheet, Automa needs to have access to the spreadsheet first. To give access, you can click the share button at the top right and then at the "Add people" form input `service@automa2.iam.gserviceaccount.com`

![Share](https://res.cloudinary.com/chat-story/image/upload/v1642067522/automa/chrome_9iHTFjxWEn_lzavjy.png)

## Loop data

Use this block to loop through data from data columns, numbers, google sheets, or use your custom data from a JSON or CSV file. After you input the data, the current iteration data will be available in the next block, and to access it write `{{ loopData@loopID.path }}` in an input.

Replace the `loopID` with the ID of the loop, you can find it on the left side when clicking the edit button of the loop data block. Make sure when you input the data it's [JSON](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON) syntax, for example, if the data that you input is an array of objects like this
```JSON
[
  { "name": "foo bar", "age": 20 },
  { "name": "bar foo", "age": 21 }
]
```
to access the data of the iteration write `{{ loopData@loopID.name }}` and the output would be `foo bar` and in the next iteration, the output would be `bar foo` and so on until the last entry. If you want to access the full object you can write `{{loopData@loopID}}` and the output would be `{ "name": "foobar", "age": 20 }`. And You can set how much data that the block should loop at the max data input.

You can learn more on [Reference Data](https://github.com/Kholid060/automa/wiki/Features#reference-data);

## Loop breakpoint

After you're using the [loop data block](https://github.com/Kholid060/automa/wiki/Blocks/_edit#loop-data), this block will tell where the loop data block must stop. You must fill the loop ID at the provided input, so can it know which Loop data blocks it must stop. 

Like when you have a workflow like this

<img src="https://i.ibb.co/xjdpvnZ/image.png" align="center" style="width: 100%" />

When the workflow reaches the loop breakpoint block. If it's the last iteration, the loop breakpoint will tell the workflow to execute the next block and if it doesn't it tells the workflow to execute the next block of the Loop data block at this case is the new tab block. And it will do this over and over until the last iteration.
