# Storybook Svelte nullish coalescing bug reproduction

This is a reproduction for https://github.com/storybookjs/storybook/issues/21705

To view the reproduction:

1. Run `yarn`.

1. Run `yarn storybook`.

1. Notice the differences between doc pages for `Button.svelte` (nearly
   unchanged from template) and `BrokenButton.svelte` (identical to
   `Button.svelte` but with one extra line in the script block:

   ```js
   const anyExpression = "with a nullish coalescing oeprator" ?? "breaks docs";
   ```

   Specifically: the description does not appear and the args table lacks any
   information that it otherwise would have parsed from the Svelte component.

After this, you can do the following to pinpoint the source of the bug:

1. Shut down the storybook server with <kbd>Ctrl</kbd> + <kbd>C</kbd>.

1. To edit the `ecmaVersion` supported by `sveltedoc-parser`, run the following:

   ```sh
   sed -i.bak 's/ecmaVersion: 9/ecmaVersion\: 11/' node_modules/sveltedoc-parser/lib/options.js
   ```

1. Run `yarn storybook` to restart Storybook.

1. Notice that the `Button.svelte` and `BrokenButton.svelte` docs are now
   identical.
