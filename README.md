# mdc-dropzone
[![build](https://travis-ci.org/moudicat/mdc-dropzone.svg?branch=master)](https://travis-ci.org/moudicat/mdc-dropzone)
[![npm](https://img.shields.io/npm/v/mdc-dropzone.svg)](https://www.npmjs.com/package/mdc-dropzone)
[![David](https://img.shields.io/david/moudicat/mdc-dropzone.svg)](https://github.com/moudicat/mdc-dropzone)
[![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/moudicat/mdc-dropzone/master/LICENSE)


A vue based dropzone component.


[![intro](https://raw.githubusercontent.com/moudicat/mdc-dropzone/master/gifs/intro.gif)](https://raw.githubusercontent.com/moudicat/mdc-dropzone/master/gifs/intro.gif)


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

## Options
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
