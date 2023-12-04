---
title: 'Component Story Format (CSF)'
---

<YouTubeCallout id="uH9_dfc-6Kc" title="Test components the EASY way | Component Story Format 3" />

Component Story Format (CSF) is the recommended way to [write stories](../writing-stories/index.md). It's an [open standard](https://github.com/ComponentDriven/csf) based on ES6 modules that is portable beyond Storybook.

<Callout variant="info" icon="💡">

If you are writing stories in the older `storiesOf()` syntax, you can find documentation in an [advanced README](https://github.com/storybookjs/storybook/blob/next/code/lib/preview-api/docs/storiesOf.md).

</Callout>

In CSF, stories and component metadata are defined as ES Modules. Every component story file consists of a required [default export](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export#Using_the_default_export) and one or more [named exports](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/export).

CSF is supported in all frameworks except React Native, where you should use the [storiesOf API](https://github.com/storybookjs/storybook/blob/next/code/lib/preview-api/docs/storiesOf.md) instead.

## Default export

The default export defines metadata about your component, including the `component` itself, its `title` (where it will show up in the [navigation UI story hierarchy](../writing-stories/naming-components-and-hierarchy.md#sorting-stories)), [decorators](../writing-stories/decorators.md), and [parameters](../writing-stories/parameters.md).

The `component` field is required and used by addons for automatic prop table generation and display of other component metadata. The `title` field is optional and should be unique (i.e., not re-used across files).

<CodeSnippets
paths={[
'angular/my-component-story-mandatory-export.ts.mdx',
'web-components/my-component-story-mandatory-export.js.mdx',
'web-components/my-component-story-mandatory-export.ts.mdx',
'common/my-component-story-mandatory-export.js.mdx',
'common/my-component-story-mandatory-export.ts.mdx',
]}
/>

For more examples, see [writing stories](../writing-stories/index.md).

## Named story exports

With CSF, every named export in the file represents a story object by default.

<CodeSnippets
paths={[
'react/my-component-story-basic-and-props.js.mdx',
'react/my-component-story-basic-and-props.ts.mdx',
'vue/my-component-story-basic-and-props.js.mdx',
'vue/my-component-story-basic-and-props.ts.mdx',
'svelte/my-component-story-basic-and-props.js.mdx',
'angular/my-component-story-basic-and-props.ts.mdx',
'web-components/my-component-story-basic-and-props.js.mdx',
'web-components/my-component-story-basic-and-props.ts.mdx',
'solid/my-component-story-basic-and-props.js.mdx',
'solid/my-component-story-basic-and-props.ts.mdx',
]}
usesCsf3
csf2Path="api/csf#snippet-my-component-story-basic-and-props"
/>

The exported identifiers will be converted to "start case" using Lodash's [startCase](https://lodash.com/docs/#startCase) function. For example:

| Identifier       |  Transformation   |
| ---------------- | :---------------: |
| name             |       Name        |
| someName         |     Some Name     |
| someNAME         |     Some NAME     |
| some_custom_NAME | Some Custom NAME  |
| someName1234     | Some Name 1 2 3 4 |

We recommend that all export names to start with a capital letter.

Story objects can be annotated with a few different fields to define story-level [decorators](../writing-stories/decorators.md) and [parameters](../writing-stories/parameters.md), and also to define the `name` of the story.

Storybook's `name` configuration element is helpful in specific circumstances. Common use cases are names with special characters or Javascript restricted words. If not specified, Storybook defaults to the named export.

<CodeSnippets
paths={[
'angular/my-component-story-with-storyname.ts.mdx',
'web-components/my-component-story-with-storyname.js.mdx',
'web-components/my-component-story-with-storyname.ts.mdx',
'common/my-component-story-with-storyname.js.mdx',
'common/my-component-story-with-storyname.ts.mdx',
]}
usesCsf3
csf2Path="api/csf#snippet-my-component-story-with-storyname"
/>

## Args story inputs

Starting in SB 6.0, stories accept named inputs called Args. Args are dynamic data that are provided (and possibly updated by) Storybook and its addons.

Consider Storybook’s ["Button" example](../writing-stories/index.md#defining-stories) of a text button that logs its click events:

<CodeSnippets
paths={[
'react/button-story-click-handler.js.mdx',
'react/button-story-click-handler.ts.mdx',
'vue/button-story-click-handler.2.js.mdx',
'vue/button-story-click-handler.2.ts.mdx',
'vue/button-story-click-handler.3.js.mdx',
'vue/button-story-click-handler.3.ts.mdx',
'svelte/button-story-click-handler.js.mdx',
'angular/button-story-click-handler.ts.mdx',
'web-components/button-story-click-handler.js.mdx',
'web-components/button-story-click-handler.ts.mdx',
'solid/button-story-click-handler.js.mdx',
'solid/button-story-click-handler.ts.mdx',
]}
usesCsf3
csf2Path="api/csf#snippet-button-story-click-handler"
/>

Now consider the same example, re-written with args:

<CodeSnippets
paths={[
'react/button-story-click-handler-args.js.mdx',
'react/button-story-click-handler-args.ts.mdx',
'vue/button-story-click-handler-args.2.js.mdx',
'vue/button-story-click-handler-args.2.ts.mdx',
'vue/button-story-click-handler-args.3.js.mdx',
'vue/button-story-click-handler-args.3.ts.mdx',
'angular/button-story-click-handler-args.ts.mdx',
'svelte/button-story-click-handler-args.js.mdx',
'web-components/button-story-click-handler-args.js.mdx',
'web-components/button-story-click-handler-args.ts.mdx',
'solid/button-story-click-handler-args.js.mdx',
'solid/button-story-click-handler-args.ts.mdx',
]}
usesCsf3
csf2Path="api/csf#snippet-button-story-click-handler-args"
/>

Or even more simply:

<CodeSnippets
paths={[
'react/button-story-click-handler-simplificated.js.mdx',
'react/button-story-click-handler-simplificated.ts.mdx',
'angular/button-story-click-handler-simplificated.ts.mdx',
'vue/button-story-click-handler-simplificated.js.mdx',
'vue/button-story-click-handler-simplificated.ts.mdx',
'web-components/button-story-click-handler-simplificated.js.mdx',
'web-components/button-story-click-handler-simplificated.ts.mdx',
'solid/button-story-click-handler-simplificated.js.mdx',
'solid/button-story-click-handler-simplificated.ts.mdx',
]}
usesCsf3
csf2Path="api/csf#snippet-button-story-click-handler-simplificated"
/>

Not only are these versions shorter and more accessible to write than their no-args counterparts, but they are also more portable since the code doesn't depend on the actions addon specifically.

For more information on setting up [Docs](../writing-docs/index.md) and [Actions](../essentials/actions.md), see their respective documentation.

## Play function

Storybook's `play` functions are small snippets of code executed when the story renders in the UI. They are convenient helper methods to help you test use cases that otherwise weren't possible or required user intervention.

A good use case for the `play` function is a form component. With previous Storybook versions, you'd write your set of stories and had to interact with the component to validate it. With Storybook's play functions, you could write the following story:

<CodeSnippets
paths={[
'react/login-form-with-play-function.js.mdx',
'react/login-form-with-play-function.ts.mdx',
'angular/login-form-with-play-function.ts.mdx',
'vue/login-form-with-play-function.js.mdx',
'vue/login-form-with-play-function.ts.mdx',
'web-components/login-form-with-play-function.js.mdx',
'web-components/login-form-with-play-function.ts.mdx',
'svelte/login-form-with-play-function.js.mdx',
'solid/login-form-with-play-function.js.mdx',
'solid/login-form-with-play-function.ts.mdx',
]}
usesCsf3
csf2Path="api/csf#snippet-login-form-with-play-function"
/>

When the story renders in the UI, Storybook executes each step defined in the `play` function and runs the assertions without the need for user interaction.

## Custom render functions

Starting in Storybook 6.4, you can write your stories as JavaScript objects, reducing the boilerplate code you need to generate to test your components, thus improving functionality and usability. `Render` functions are helpful methods to give you additional control over how the story renders. For example, if you were writing a story as an object and you wanted to specify how your component should render, you could write the following:

<CodeSnippets
paths={[
'react/component-story-with-custom-render-function.js.mdx',
'react/component-story-with-custom-render-function.ts.mdx',
'angular/component-story-with-custom-render-function.ts.mdx',
'vue/component-story-with-custom-render-function.js.mdx',
'vue/component-story-with-custom-render-function.ts.mdx',
'preact/component-story-with-custom-render-function.js.mdx',
'web-components/component-story-with-custom-render-function.js.mdx',
'web-components/component-story-with-custom-render-function.ts.mdx',
'solid/component-story-with-custom-render-function.js.mdx',
'solid/component-story-with-custom-render-function.ts.mdx',
]}
usesCsf3
/>

When Storybook loads this story, it will detect the existence of a `render` function and adjust the component rendering accordingly based on what's defined.

## Storybook export vs. name handling

Storybook handles named exports and the `name` option slightly differently. When should you use one vs. the other?

Storybook will always use the named export to determine the story ID and URL.

If you specify the `name` option, it will be used as the story display name in the UI. Otherwise, it defaults to the named export, processed through Storybook's `storyNameFromExport` and `lodash.startCase` functions.

<CodeSnippets
paths={[
'common/storybook-test-with-storyname.js.mdx',
]}
/>

When you want to change the name of your story, rename the CSF export. It will change the name of the story and also change the story's ID and URL.

It would be best if you used the `name` configuration element in the following cases:

1. You want the name to show up in the Storybook UI in a way that's not possible with a named export, e.g., reserved keywords like "default", special characters like emoji, spacing/capitalization other than what's provided by `storyNameFromExport`.
2. You want to preserve the Story ID independently from changing how it's displayed. Having stable Story IDs is helpful for integration with third-party tools.

## Non-story exports

In some cases, you may want to export a mixture of stories and non-stories (e.g., mocked data).

You can use the optional configuration fields `includeStories` and `excludeStories` in the default export to make this possible. You can define them as an array of strings or regular expressions.

Consider the following story file:

<CodeSnippets
paths={[
'react/my-component-story-with-nonstory.js.mdx',
'react/my-component-story-with-nonstory.ts.mdx',
'vue/my-component-story-with-nonstory.js.mdx',
'vue/my-component-story-with-nonstory.ts.mdx',
'svelte/my-component-story-with-nonstory.js.mdx',
'angular/my-component-story-with-nonstory.ts.mdx',
'web-components/my-component-story-with-nonstory.js.mdx',
'web-components/my-component-story-with-nonstory.ts.mdx',
'solid/my-component-story-with-nonstory.js.mdx',
'solid/my-component-story-with-nonstory.ts.mdx',
]}
usesCsf3
csf2Path="api/csf#snippet-my-component-story-with-nonstory"
/>

When this file renders in Storybook, it treats `ComplexStory` and `SimpleStory` as stories and ignores the `data` named exports.

For this particular example, you could achieve the same result in different ways, depending on what's convenient:

- `includeStories: /^[A-Z]/`
- `includeStories: /.*Story$/`
- `includeStories: ['SimpleStory', 'ComplexStory']`
- `excludeStories: /^[a-z]/`
- `excludeStories: /.*Data$/`
- `excludeStories: ['simpleData', 'complexData']`

The first option is the recommended solution if you follow the best practice of starting story exports with an uppercase letter (i.e., use UpperCamelCase).

## Upgrading from CSF 2 to CSF 3

In CSF 2, the named exports are always functions that instantiate a component, and those functions can be annotated with configuration options. For example:

<CodeSnippets
paths={[
'react/csf-2-example-starter.js.mdx',
'react/csf-2-example-starter.ts.mdx',
'vue/csf-2-example-starter.2.js.mdx',
'vue/csf-2-example-starter.2.ts.mdx',
'vue/csf-2-example-starter.3.js.mdx',
'vue/csf-2-example-starter.3.ts.mdx',
'angular/csf-2-example-starter.ts.mdx',
'web-components/csf-2-example-starter.js.mdx',
'web-components/csf-2-example-starter.ts.mdx',
'solid/csf-2-example-starter.js.mdx',
'solid/csf-2-example-starter.ts.mdx',
]}
/>

This declares a Primary story for a Button that renders itself by spreading `{ primary: true }` into the component. The `default.title` metadata says where to place the story in a navigation hierarchy.

Here's the CSF 3 equivalent:

<CodeSnippets
paths={[
'common/csf-3-example-starter.js.mdx',
'react/csf-3-example-starter.ts.mdx',
'vue/csf-3-example-starter.ts.mdx',
'angular/csf-3-example-starter.ts.mdx',
'web-components/csf-3-example-starter.js.mdx',
'web-components/csf-3-example-starter.ts.mdx',
'solid/csf-3-example-starter.ts.mdx',
]}
/>

Let's go through the changes individually to understand what's going on.

### Spreadable story objects

In CSF 3, the named exports are **objects**, not functions. This allows us to reuse stories more efficiently with the JS spread operator.

Consider the following addition to the intro example, which creates a `PrimaryOnDark` story that renders against a dark background:

Here's the CSF 2 implementation:

<CodeSnippets
paths={[
'common/csf-2-example-primary-dark-story.js.mdx'
]}
/>

`Primary.bind({})` copies the story function, but it doesn't copy the annotations hanging off the function, so we must add `PrimaryOnDark.args = Primary.args` to inherit the args.

In CSF 3, we can spread the `Primary` object to carry over all its annotations:

<CodeSnippets
paths={[
'common/csf-3-example-primary-dark-story.js.mdx',
'common/csf-3-example-primary-dark-story.ts.mdx',
]}
/>

Learn more about [named story exports](#named-story-exports).

### Default render functions

In CSF 3, you specify how a story renders through a `render` function. We can rewrite a CSF 2 example to CSF 3 through the following steps.

Let's start with a simple CSF 2 story function:

<CodeSnippets
paths={[
'react/csf-2-example-story.js.mdx',
'react/csf-2-example-story.ts.mdx',
'vue/csf-2-example-story.2.js.mdx',
'vue/csf-2-example-story.2.ts.mdx',
'vue/csf-2-example-story.3.js.mdx',
'vue/csf-2-example-story.3.ts.mdx',
'angular/csf-2-example-story.ts.mdx',
'web-components/csf-2-example-story.js.mdx',
'web-components/csf-2-example-story.ts.mdx',
'solid/csf-2-example-story.js.mdx',
'solid/csf-2-example-story.ts.mdx',
]}
/>

Now, let's rewrite it as a story object in CSF 3 with an explicit `render` function that tells the story how to render itself. Like CSF 2, this gives us full control of how we render a component or even a collection of components.

<CodeSnippets
paths={[
'react/csf-3-example-render.js.mdx',
'react/csf-3-example-render.ts.mdx',
'vue/csf-3-example-render.2.js.mdx',
'vue/csf-3-example-render.2.ts.mdx',
'vue/csf-3-example-render.3.js.mdx',
'vue/csf-3-example-render.3.ts.mdx',
'angular/csf-3-example-render.ts.mdx',
'web-components/csf-3-example-render.js.mdx',
'web-components/csf-3-example-render.ts.mdx',
'solid/csf-3-example-render.js.mdx',
'solid/csf-3-example-render.ts.mdx',
]}
/>

Learn more about [render functions](#custom-render-functions).

But in CSF 2, a lot of story functions are identical: take the component specified in the default export and spread args into it. What's interesting about these stories is not the function, but the args passed into the function.

CSF 3 provides default render functions for each renderer. If all you're doing is spreading args into your component—which is the most common case—you don't need to specify any `render` function at all:

<CodeSnippets
paths={[
'common/csf-3-example-default-render.js.mdx'
]}
/>

For more information, see the section on [custom render functions](#custom-render-functions).

### Generate titles automatically

Finally, CSF 3 can automatically generate titles.

<CodeSnippets
paths={[
'common/csf-2-example-title.js.mdx'
]}
/>

<CodeSnippets
paths={[
'common/csf-3-example-auto-title.js.mdx'
]}
/>

You can still specify a title like in CSF 2, but if you don't specify one, it can be inferred from the story's path on disk. For more information, see the section on [configuring story loading](../configure/index.md#configure-story-loading).