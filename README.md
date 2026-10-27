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

## Unnecessary Tools Workshop

The page also includes twenty interactive mini-tools: File Airport Security, HTML Courtroom, File Washing Machine, Loading Bar Olympics, File Dating Simulator, The Overthinking Button, Digital Plant Care, File Escape Room, The Bureaucracy Generator, HTML Fashion Show, The Digital Pet Rock, File Fishing, The Productivity Slot Machine, The File Talent Show, The Unnecessary Password Generator, The Mouse Olympics, The Digital Time Machine, The HTML Detective, The Digital Weather Station, and The Undo Museum.

The workshop has a searchable directory grouped into Games, File Tools, HTML Tools, and Just for Fun. Each tool opens as its own in-page view and has a `#tool/<name>` deep link. **Random tool** and **Surprise Me** choose from the currently visible directory results. The **Make This Task Unnecessarily Complicated** flow supports uploading the selected file, formatting the courtroom HTML, or copying overthinking text; its Skip button runs the chosen action immediately.

Shared achievements, tool visits, statistics, and personal bests are stored locally in the browser. The achievements panel includes a reset option with a confirmation prompt. Reduced-motion preferences are respected, and the existing sound toggle remains available with a lower default volume.

The scanner, race, dating dialog, slot rewards, fictional forecasts, deliberation, and paperwork are entertainment. Airport screening does not modify the source file; its safe copy is byte-for-byte identical. The washing machine can create a separate HTML copy with trailing whitespace cleaned when that option is selected. The courtroom and fashion show have basic HTML indentation helpers. The talent show reads files locally and never executes uploaded HTML. Review generated copies before using them. Clipboard access depends on browser permissions. Plant and pet-rock progress save locally only when you choose their save buttons; Mouse Olympics keeps a local personal best. The password tool generates fictional jokes only, never credentials for real accounts. The Undo Museum records the current page session; its restore action applies only to text edits it observed, and other actions are history entries rather than reversible changes.

## Embed it

The simplest option is to serve `index.html` directly or embed it in an `<iframe>`. The widget's styles use the `oc-` prefix and its JavaScript is enclosed in an IIFE. For inline integration, the page's `<style>` block, `<section class="oc-root">`, and `<script>` block can be copied into another page; configure the upload endpoint there as described above.
