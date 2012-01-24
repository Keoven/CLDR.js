## CLDR.js

CLDR.js provides logic from the
[Unicode Common Locale Data Repository](http://cldr.unicode.org/).
Currently, the only functionality it provides is the
[pluralization rules](http://unicode.org/repos/cldr-tmp/trunk/diff/supplemental/language_plural_rules.html).


### Plural Rules

Usage:

    CLDR.pluralForm(0, 'en');     // => 'other'
    CLDR.pluralForm(1, 'en-US');  // => 'one'
    CLDR.pluralForm(2.383, 'fr'); // => 'other'
    CLDR.pluralForm(1, 'zh');     // => 'other'
    CLDR.pluralForm(26, 'uk');    // => 'many'

Though CLDR.js doens't *provide* an I18n framework, you can use this
logic as part of yours. For example, you might write the following:

    CLDR.defaultLanguage = 'en';

    var translations = {
      'en': {
        'widget': {
          'one': 'one widget',
          'other': '{{count}} widget'
        }
      },
      'jp': {
        'widget': {
          'other': '{{count}} ウィジェット'
        }
      }
    };

    function pluralize(key, count) {
      var form = CLDR.pluralForm(count);
      return translations[CLDR.defaultLanguage][key][form];
    }