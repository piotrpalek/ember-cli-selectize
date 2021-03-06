# Ember-cli-selectize

An Ember and Selectize integration, packaged as an Ember-cli addon. Check [Selectize](http://brianreavis.github.io/selectize.js/) and [Ember-cli](http://www.ember-cli.com/)!

## Demo

Check (old demo): http://miguelcobain.github.io/ember-selectize

## Browser Support

Should run wherever Ember and Selectize run.

## Installation

### As an Ember CLI addon (0.1.5 or later)

Run `ember install:addon ember-cli-selectize` on your project folder.

### As an Ember CLI addon (prior to 0.1.5)

Run `npm install --save-dev ember-cli-selectize` on your project folder.

Run `ember g ember-cli-selectize` to install selectize dependency from bower.

### As a Standalone Library

Download a [release][releases].

[releases]: https://github.com/miguelcobain/ember-cli-selectize/releases

Copy to your vendor directory and link up the .js file.

## Usage

This addon provides an `ember-selectize` component.
Its usage should be very similar to `Ember.Select`, but with additional features.

```handlebars
{{ember-selectize
  content=controller.items
  optionValuePath="content.id"
  optionLabelPath="content.name"
  selection=model.item
  placeholder="Select an item" }}
```

### Properties

- `content` - Array containing all the options to select from
- `selection` - Ember-selectize will set this property to the selection that was made. Usually some property on a model, for example. If `multiple` is `true`, then it should be an array.
- `value` - Ember-selectize will set this property to the *value of the selection* that was made. It is not currently supported in multiple selection mode.
- `optionValuePath` - Selectize requires a unique hash for each option available. Set this to a path to such a property on your options. Prefix with `content.`. Example: `content.id`
- `optionLabelPath` - Set this to a path where selectize can get a label for display. Computed properties are many times useful for this. Example: `content.name`
- `plugins` - Set this to a comma delimited list of selectize plugins to override the default plugin selection (currently remove_button). Note, not all plugins have been tested to work with ember-cli-selectize, YMMV. Example: `restore_on_backspace,drag_drop`
- `placeholder` or `prompt` - Set any of these to display a text when there is no choice made. Example `"Please select an- option"`
- `disabled` - If `true` disables changes in selectize
- `multiple` - If `true` ember-selectize will enter multiple mode. `selection` is an array of options.
- `maxItems` - If `multiple` is true, you can optionally set this to limit the number of selections.
- `sortField` - Pass a string of a property to sort by. You can also pass an array of objects `[{ field: 'someProperty', direction: 'asc' }, {/*...*/}]`. See [selectize usage](https://github.com/brianreavis/selectize.js/blob/master/docs/usage.md) for details. Example: `"name"`
- `sortDirection` - If `sortField` is a string, specify the direction. Example: `"asc"` or `"desc"`. This is ignored if `sortField` is an array (you can specify direction inside that array).
- `create` - Pass a string to 'create' property to enable tag creation mode. When active, ember-selectize will send an action with that name to the application when a tag is created. The text is sent as a parameter.
- `filter` - This property will have the text that the user entered to filter options. Useful for searching options in server from a large set.
- `loading` - When `true` ember-selectize adds a loading class to selectize wrapper. Just like selectize does. Then you can customize. Useful with async relationships or "finds" in Ember-Data: `loading=types.isPending`.
- `loadingClass` - Customize the loading class name. Default value: `loading`
- `optionFunction`, `itemFunction`, `optionCreateFunction`, `optgroupHeaderFunction`, `optgroupFunction`  - Will be called on the component with two parameters `data` and `escape`, `escape` is a function to escape text. these functions are expected to build the desired html and return it as a string. These functions take precedence over `optionTemplate`,`itemTemplate`,`optionCreateTemplate`,`optgroupHeaderTemplate`,`optgroupTemplate` `optionView`,`itemView`,`optionCreateView`,`optgroupHeaderView` and `optgroupView`.
- `optionTemplate`,`itemTemplate`,`optionCreateTemplate`,`optgroupHeaderTemplate`,`optgroupTemplate` `optionView`,`itemView`,`optionCreateView`,`optgroupHeaderView` and `optgroupView` - Render using templates or views! View takes precedence over template, so if you do strange things like setting optionView and optionTemplate, the latter will be ignored. Might not work with all Ember versions. This is delicate. Check [this issue](https://github.com/miguelcobain/ember-selectize/issues/13#issuecomment-56155784).
- `required` - If `true` adds `required` attribute
- `closeAfterSelect` - If `true` the dropdown will be closed after a selection is made.

More info:
- ember-selectize registers observers on object labels. This is great because if you change the label property anywhere in your application, selectize labels will also update.

### Theme customization

You can customize which theme to use in your Brocfile.
```javascript
//your-app/Brocfile.js

var EmberApp = require('ember-cli/lib/broccoli/ember-app');

var app = new EmberApp({
  'ember-cli-selectize': {
    //valid values are `default`, `bootstrap2`, `bootstrap3` or false
    'theme': 'bootstrap3'
  }
});

module.exports = app.toTree();
```

If you want to use the default theme, you don't need to specify any option.
If you don't want to include any css at all for some reason, simply assign `false` or any "falsy" value to the `theme` option.

## Running

* `ember server`
* Visit your app at http://localhost:4200.

## Running Tests

* `ember test`
* `ember test --server`

Tests are written in qunit, and some were borrowed from `Ember.Select`.

I've rewritten many of them, but most of them still fail.

This is due to the nature of this component. `Selectize`'s tests assures that everything is ok between Selectize<->DOM.
`Ember.Select`'s tests also test the DOM. This is unecessary in this project.

Ember-selectize tests should be focused between Ember<->Selectize.

## Building

* `ember build`

For more information on using ember-cli, visit [http://www.ember-cli.com/](http://www.ember-cli.com/).
