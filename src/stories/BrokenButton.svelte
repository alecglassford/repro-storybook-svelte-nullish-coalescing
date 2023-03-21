<script>
  /**
   * This description will render at the top of the Button doc, but not the
   * BrokenButton doc.
   * @component
   */

  import './button.css';

  /**
   * Is this the principal call to action on the page?
   */
  export let primary = false;

  /**
   * @type {string} What background color to use
   */
  export let backgroundColor = undefined;

  /**
   * @type {'small' | 'medium' | 'large'} How large should the button be?
   */
  export let size = 'medium';

  /**
   * @type {string} Button contents
   */
  export let label;

  $: mode = primary ? 'storybook-button--primary' : 'storybook-button--secondary';

  $: style = backgroundColor ? `background-color: ${backgroundColor}` : '';

  const anyExpression = "with a nullish coalescing oeprator" ?? "breaks docs";
</script>

<button
  type="button"
  class={['storybook-button', `storybook-button--${size}`, mode].join(' ')}
  {style}
  on:click
>
  {label}
</button>
