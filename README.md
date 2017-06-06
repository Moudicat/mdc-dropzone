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
import Dropzone from 'mdc-dropzone';

...in script
components: { Dropzone }

...in html
<Dropzone url="https://xxx.com/upload"></Dropzone>
```

## Usage
### props
| name            | type         |  default           |  desc       |
|:---------:|:---------:|:------------:|:-----------:|
| url                | String       |   null (required)    |  upload api url
| limitInMB      |   Number   |   5                      | size limit of receive files

### event
| name            |   desc       | params
|:---------:|:-----------:|
| onSuccess   |   All file uploaded. |  xhr.response
| onError       |   upload error.       |  xhr
| onProgress  |  upload Progress.  |  progress, current file
| dragenter    |   drag enter .         | -
| dragleave    |   drag leave .         | -


## Still working on it!