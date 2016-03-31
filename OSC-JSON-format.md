This document describes the standard Open Supernova Catalog (OSC) JSON format. For JSON files in this repository, which are mostly entered by hand or via data donations, our format requirements are less strict than usual, for instance if you forget to set a supernova's name field, our import script is smart enough to do this for you. As JSON is a sparse format, object names that don't follow our default name choices will simply be ignored by the script. In most cases, this is not desirable as you will want your data to be readable by the catalog import script, but it can be useful for adding new objects that may be unique to your dataset, which in the future could be parsed by the catalog. But so long as you are only adding standard data to a supernova, it is best to follow the guidelines set in this document as closely as possible to avoid potential issues.

Each supernova is contained with a single JSON file that contains a single object bearing the supernova's primary name, which when empty represents the minimum readable entry file:

```JSON
{
	"SN1987A":{}
}
```

To comply with the standard, the object should contain a "name" key and an "aliases" array, where the "name" key should be identical to the primary object name. The aliases array should also contain the supernova's name, as well as any other names the supernova is known by:

```JSON
{
	"SN1987A":{
		"name":"SN1987A",
		"aliases":[
			"SN1987A"
		]
	}
}
```

Sources are extremely important in the OSC, and every single piece of data added to an event JSON file **must have a source attribution**, with the sole exception of the supernova name, aliases, and the sources themselves. Published data sources are preferred over secondary sources (the OSC falls into a secondary source category), but if the data was collected by a secondary source intermediate to being added to the OSC, these sources should also be attributed in the source list.

Sources of data contain five fields, three of which are optional:

| Field | Value | Optional?
| :--- | :--- | :---
`name` | Source name, e.g. "Catchpole et al. 1989" | no
`alias` | Integer unique to this source to be used as an alias | no
`url` | Web address of source | yes
`bibcode` | 19 character NASA ADS bibcode | yes
`secondary` | Boolean specifying if source collected rather than generated data | yes

The sources object contains an array of such objects:

```JSON
"sources":[
	{
		"name":"Catchpole et al. (1987)",
		"url":"http://adsabs.harvard.edu/abs/1987MNRAS.229P..15C",
		"bibcode":"1987MNRAS.229P..15C",
		"alias":"1"
	},
	{
		"name":"SUSPECT",
		"url":"https://www.nhn.ou.edu/~suspect/",
		"alias":"2",
		"secondary":true
	}
]
```

Data quanta are added to each event as arrays of objects, with each piece of datum being tagged with its associated sources' alias tags. An example tag might be an event's redshift,

```JSON
"redshift":[
	{
		"value":"0.045",
		"error":"0.001",
		"source":"1,2"
	},
	{
		"value":"0.043",
		"error":"0.002",
		"source":"3"
	}
]
```

where in this example we have two different redshift values quoted from three different sources, where two of the sources agree with one another. Note that all the numerical values are stored as strings instead of as numbers, our policy is to store the data with exactly the same number of significant digits as the sources that provide them, and storing the importing the data as floating point numbers can often introduce small floating-point errors that we wish to avoid.

Data quanta have four standard fields:

| Field | Value | Optional?
| :--- | :--- | :---
| `value` | The value of the quanta | no
| `error` | The error associated with the value | yes
| `unit` | The unit of the value | yes
| `source` | A list of integer aliases to sources for the data | no

Photometry and spectra are stored in a similar way, but have different and many more standard field names. For photometry, the standard field names are:

| Field | Value | Optional?
| :--- | :--- | :---
| `time` | Time of observation | yes
| `e_time` | Error in the time | yes
| `timeunit` | Unit for time | yes
| `magnitude` | Apparent magnitude | no
| `e_magnitude` | Error in the magnitude | yes
| `band` | Photometric band filter | yes
| `upperlimit` | Measurement is upper limit | yes
| `system` | Photometric system used | yes
| `instrument` | Instrument used for observation | yes
| `telescope` | Telescope used for observation | yes
| `observatory` | Observatory used for observation | yes
| `observer` | Person(s) who conducted the observation | yes
| `source` | A list of integer aliases to sources for the data | no

For spectra:

| Field | Value | Optional?
| :--- | :--- | :---
| `time` | Time of observation | yes
| `e_time` | Error in the time | yes
| `data` | Nx2 or Nx3 array of wavelengths, fluxes, and (optionally) errors | no
| `timeunit` | Unit for time | yes
| `waveunit` | Unit for wavelength | no
| `fluxunit` | Unit for fluxes | no
| `snr` | Signal to noise ratio | yes
| `filename` | Name of file spectra was extracted from | yes
| `deredshifted` | Data is known to have been deredshifted from observer frame | yes
| `dereddened` | Data is known to have been dereddened | yes
| `instrument` | Instrument used for observation | yes
| `telescope` | Telescope used for observation | yes
| `observatory` | Observatory used for observation | yes
| `observer` | Person(s) who conducted the observation | yes
| `reducer` | Person(s) who reduced the observation | yes
| `source` | A list of integer aliases to sources for the data | no
