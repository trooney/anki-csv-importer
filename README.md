# Anki CSV Importer

Imports a local CSV file into an Anki deck. It supports a flexible notion of note types and alternatives to the default primary card identifier.

This fork began as a script by Gulshan Singh <gsingh2011@gmail.com> and contains modifications by Tyler Rooney <tyler@tylerroney.ca>.

## Usage

```
usage: anki-csv-importer.py [-h] -p PATH -d DECK -n NOTE

Import a local or remote CSV file into Anki

optional arguments:
  -h, --help            show this help message and exit
  -p PATH, --path PATH  the path of the local CSV file
  -d DECK, --deck DECK  the name of the deck to import the sheet to
  -n NOTE, --note NOTE  the note type to import
```

## Instructions

### Usage

`./anki-csv-importer.py --path "<path>" --deck "<deck_name>" --note "<note_type>"`

A sync is automatically run after the notes are added.

### Integration with AnkiConnect

The first row of the CSV must contain the names of the fields of the note type, and it may optionally contain 'Tags' to specify which column should be used for tags.

For example, if the note has the three fields `question`, `answer`, `some_field`, then the CSV file should look something like

```
Question,Answer,Some Field,Tags
question1,answer1,some_field1,tags1
question2,answer2,some_field1,tags1
...
```

## HTML Formatting

HTML formatting is enabled when using AnkiConnect and currently cannot be disabled.

To display HTML as plaintext when HTML formatting is enabled is enabled, you can use [HTML escape entities](https://www.w3schools.com/html/html_entities.asp). For example, to display `<b>` as plaintext, you would enter `&lt;b&gt;`.

## How sheet modifications are handled

This is the default behavior of Anki's `TextImporter`:

- When a new row is added or the "primary field" (i.e. "Front") is changed in the Google Sheet, a new note is added to the Anki deck
- When any column other than the "primary field" is updated in the Google Sheet, the note in the deck is updated with the new fields. Review time does not change.
- When a row is deleted, it's not deleted from the Anki deck

## License

[MIT](./LICENSE)
