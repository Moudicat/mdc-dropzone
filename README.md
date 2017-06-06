# mdc-dropzone
A vue based dropzone component.

## How to use

```
yarn install mdc-dropzone
```
or
```
npm install mdc-dropzone
```

```
import dropzone from 'mdc-dropzone';

...in script
components: { dropzone }

...in html
<dropzone url="https://xxx.com/upload"></dropzone>
```

## Usage
### props
| name        | type       |  default            |  desc                              |
|:-----------:|:----------:|:-------------------:|:----------------------------------:|
| url         |   String   |   null (required)   | upload api url                     |
| method      |   String   |   post              | you can use `put` instead of `post`|
| headers     |   Object   |   {}                | eg. {'X-Token': '12345678'}        |
| limitInMB   |   Number   |   5                 | size limit of receive files        |
| limitFiles  |   Number   |   10                | limit number of files              |



### event
| name         |   desc               | params                       |
|:------------:|:--------------------:|:----------------------------:|
| onSuccess    |  All file uploaded.  |  xhr.response                |
| onError      |  upload error.       |  xhr                         |
| onProgress   |  upload Progress.    |  progress, current file name |
| onDragenter  |  drag enter .        |  ev                          |
| onDragleave  |  drag leave .        |  ev                          |
| onDrop       |  drop .              |  ev                          |

## Still working on it!
