# vue-fineuploader-dropzone

[![Build Status](https://travis-ci.org/Elhebert/vue-fineuploader-dropzone.svg?branch=master)](https://travis-ci.org/Elhebert/vue-fineuploader-dropzone)
[![Dependency Status](https://david-dm.org/Elhebert/vue-fineuploader-dropzone.svg)](https://david-dm.org/Elhebert/vue-fineuploader-dropzone)
[![devDependency Status](https://david-dm.org/Elhebert/vue-fineuploader-dropzone/dev-status.svg)](https://david-dm.org/Elhebert/vue-fineuploader-dropzone?type=dev)


## New Version In Progress

I'm refactoring the `vue-fineuploader` component to be more customisable and to use all the options that fineuploader offer.
You can see the **WIP** here [vue-fineuploader/feature/refactor](https://github.com/Elhebert/vue-fineuploader/tree/feature/refactor). This new version is based on the react components (https://github.com/FineUploader/react-fine-uploader).

It'll offer a wrapper for each endpoints of fineuploader, and a component for all the UI options (dropzone, fileinput, cancel-button, ...).

This component won't be updated or supported after it's released.


Be sure to check it out, and help in anyway you can, porting a component or the documenation, everyone can help !

ETA: end of January.

## The release candidate of vue-fineuploader v2.0.0 has been released

[Release notes](https://github.com/FineUploader-transfer/vue-fineuploader/releases/tag/v2.0.0-rc.1)

This repository is now outdated, and the package won't be supported anymore.

---

A VueJS 2 Component for Fine Uploader with a drag'n'drop area.

For the core version (without the drag'n'drop support) see: [https://github.com/Elhebert/vue-fineuploader](https://github.com/Elhebert/vue-fineuploader)

Demo: [https://elhebert.github.io/vue-fineuploader-dropzone/](https://elhebert.github.io/vue-fineuploader-dropzone/)

## Usage

### Installation

Get the `FineUploader` component:

- with npm:
```
npm install --save vue-fineuploader-dropzone
```
- clone this repository and copy the `FineUploader.vue` into your project:
```
git clone https://github.com/Elhebert/vue-fineuploader-dropzone.git
```


### Properties

- `button`: Specify an element to use as the 'select files' button. Cannot be a `<button>`.
- `options`: Object containing the different configuration options.

For information on the possible [options](http://docs.fineuploader.com/branch/master/api/options.html) take a look at the official documentation

- `dropzone`: Object container the different dropzone options
    - `element`: id or class of the container element that should be treated as drop zone.
    - `dropActive`: Specify a CSS class to apply to drop zone(s) when a file has entered it.

### Events

From the official documentation :
> Fine Uploader's event system enables integrators to execute any operations at almost any point in the upload process. Knowing how these callbacks work, and when they are called, is crucial to unlocking the full potential of Fine Uploader.

vue-fineuploader-dropzone simply emit the different callbacks. Use the `v-on:<event>` or `@<event>` to listen to them.

In the FineUploader documentation the callbacks are functions with parameters, the events that are emitted for vue-fineuplaoder are returning a payload objects using those paramaters has key.

For example, the `onSubmit` callback has an `id` and a `name` as parameters. The `submit` event from vue-fineuploader will return the following object : `{ id: <id>, name: <name> }`.


For information on the different [events](http://docs.fineuploader.com/branch/master/api/events.html) take a look at the official documentation


#### Event naming

In the official documentation, the events are called `onEvent`, using a camelCase notation. vue-fineuploader events are using camelcase notation and don't use the prefix `on`.

For example, to listen to the `onAllComplete` callback, you need to listen to the `allcomplete` event.

### Example

```js
<template>
    <div>
        <FineUploader :button="button" 
                      :options="options" 
                      :dropZone="dropZone"
                      @submit="addFileToQueue">
            <div class="drop-area">
                Drop your files here
                <br>or<br>
                <div class="browse"></div>
            </div>
        </FineUploader>
    </div>
</template>

<style></style>

<script language="text/babel">
import FineUplaoder from './path/to/FineUploader.vue'; // If you copied the component into your project
import FineUploader from 'vue-fineuploader-dropzone'; // If you used npm to install the component

export default {
    data() {
        return {
            button: '.browse',
            options: {
                request: {
                    endpoint: '/path/to/your/endpoint'
                },
                ...
            },
            dropZone: {
                element: '.drop-area',
                dropActive: 'active'
            },
        };
    },

    components: { FineUploader },
    
    methods: {
        addFileToQueue(payload) {
            ...
        },
    },
};
</script>
```

This script is published under the [MIT license](./LICENSE)
