# sne-internal

This repository is used to store datasets that are pulled directly from historical papers that have not yet been digitized. The repository will be different from the other repositories within the OSC in that individual event files will be edited by hand, as older papers do not have actual text objects, just image scans of each page. The files in this repository should be in JSON format, but the format is not as strict as the JSON files that appear in the main catalog (they will be cleaned upon import anyway). If no source is attached to individual data objects, the first source specified is assumed to be the source of the data. Key names are identical to those in the main repo as generted by the import script.

Here's an example file for SN1937A:

```JSON
{
  "SN1937A":{
    "sources":[ { "bibcode":"1937PASP...49..204Z" } ],
    "photometry":[
      { "timeunit":"JD", "time":"2428521", "band":"Mp", "abmag":"17.5", "instrument":"18-inch Schmidt", "upperlimit":true },
      { "timeunit":"JD", "time":"2428524", "band":"Mp", "abmag":"17.5", "instrument":"18-inch Schmidt", "upperlimit":true },
      { "timeunit":"JD", "time":"2428581", "band":"Mp", "abmag":"16.2", "instrument":"18-inch Schmidt" },
      { "timeunit":"JD", "time":"2428599", "band":"Mp", "abmag":"16.7", "instrument":"18-inch Schmidt" },
      { "timeunit":"JD", "time":"2428600", "band":"Mp", "abmag":"16.5", "instrument":"18-inch Schmidt" },
      { "timeunit":"JD", "time":"2428635", "band":"Mp", "abmag":"16.9", "instrument":"18-inch Schmidt" },
      { "timeunit":"JD", "time":"2428636", "band":"Mp", "abmag":"17.2", "instrument":"18-inch Schmidt" },
      { "timeunit":"JD", "time":"2428664", "band":"Mp", "abmag":"17.5", "instrument":"18-inch Schmidt", "upperlimit":true },
      { "timeunit":"JD", "time":"2428667", "band":"Mp", "abmag":"19.3", "instrument":"18-inch Schmidt" }
    ]
  }
}
