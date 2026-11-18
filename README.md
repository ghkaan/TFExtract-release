# TFExtract-release
TFExtract
Anton Kamyshev, 2026

Extracts Table, Listing and Figure titles and footnotes from RTF/DOCX files and exports them to XLSX.

Generated XLSX contains columns SECTION (TABLE\LISTING\FIGURE), PROGNAME (program name), DATASET (dataset name), TABORD (number of the duplicate for duplicated IDs), NUMBER (subsequent number of the output), FILENAME (same as DATASET), SOURCE (for repeated outputs), TITLE1-TITLE10 and FNOTE1-FNOTE10.
If some outputs have same identifier (PROGNAME\DATASET) they will be marked with orange color.
Header line is marked with light blue color and has autofilter applied.

Output name templates:
░░[datetime] -> YYYYMMDD_HHMMSS
░░[date] -> YYYYMMDD

Default settings:

Shells section - regexp to identify start of the section with shells in the document, extraction will be started after this point:
░░(?i)^\s*(?:\d+(?:\.\d+)*\.?\s*)?(?=.*\b(?:TABLE|LISTING|FIGURE)\b)(?=.*\bSHELLS\b).*$

First title - regexp to identify first title (output name):
░░^(Table|Listing|Figure) ([0-9]+(?:\.[0-9]+)*[A-Za-z]?) +[A-Z].*$

Source - regexp to identify source output:
░░(?i)^\s*Source:\s*.*$

First footnote - regexp to identify first footnote:
░░(?i)^\s*Notes?:\s*.*$

Close footnotes - regexp to identify where footnotes should be closed (not included):
░░(?i)^\s*(?:Program:|Programming note:).*$

Repeated outputs - regexp to identify line with description of the repeat:
░░(?i)\bRepeat\s+(Table|Listing|Figure)\s+([0-9]+(?:\.[0-9]+)*[A-Za-z]?)

Repeated source - regexp to identify replacement of the source for repeated output:
░░(?i)\bChange\s+Source\s+to\b.*?((?:(?:Table|Listing|Figure)\s+[0-9]+(?:\.[0-9]+)*[A-Za-z]?)(?:\s*,\s*(?:Table|Listing|Figure)\s+[0-9]+(?:\.[0-9]+)*[A-Za-z]?)*)

Source prefix - text to be used as prefix for source replacement (in repeated source):
░░Source:

Steps:
░░1. Select an RTF or DOCX file or enter its full path.
░░2. Set the output filename and adjust regular expressions if necessary.
░░3. Click Extract or use File > Extract.
░░4. The XLSX file is saved next to the input document unless an absolute output path is specified.
