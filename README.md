# The Overcomplicator: File Uploads, Needlessly

A playful, self-contained file upload demo. Instead of a plain upload form, files can be launched through a basketball hoop or fired at a target with a catapult. There is also a regular upload button for when the games get old.

## Run it

Open `index.html` in a modern browser. No build step, package install, or external library is required.

Choose a file, drag one onto an arena, or select **use a practice file**. Score a basket or hit the catapult target to trigger an upload. You can also use the boring button to upload directly. The basketball game includes optional chaos mode; the catapult has adjustable angle and power, plus an optional trajectory guide. Sound can be muted.

## Demo mode and real uploads

By default, the page runs in demo mode: it simulates upload progress for about 1.4 seconds, records the result on the page, and sends no file over the network.

To connect a server, edit the `CONFIG` object near the top of the script in `index.html`:

```js
const CONFIG = {
  uploadUrl: '/api/upload',
  fieldName: 'file',
  headers: {}
};
```

The page sends a `POST` request with `multipart/form-data`; the file is included under `fieldName`. Optional `headers` are added to the request. The server should return a 2xx status for success. Ensure the endpoint, authentication, and any required CSRF headers match your application.

## Listen for upload results

The page dispatches a bubbling `overcomplicator:upload` event from the widget root after each attempt. Its `detail` contains the file, the method used, whether it succeeded, and any error message:

```js
document.addEventListener('overcomplicator:upload', event => {
  const { file, via, ok, error } = event.detail;
  console.log({ file, via, ok, error });
});
```

Upload methods include `File Basketball`, `File Catapult`, and `The Boring Button (shameful)`.

## Embed it

The simplest option is to serve `index.html` directly or embed it in an `<iframe>`. The widget's styles use the `oc-` prefix and its JavaScript is enclosed in an IIFE. For inline integration, the page's `<style>` block, `<section class="oc-root">`, and `<script>` block can be copied into another page; configure the upload endpoint there as described above.
