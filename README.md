# sne-internal

This repository is used to store datasets that are pulled directly from historical papers that have not yet been digitized. The repository will be different from the other repositories within the OSC in that individual event files will be edited by hand, as older papers do not have actual text objects, just image scans of each page. Each file in this repository should be prefaced with a few comments in their headers describing the data (beginning with the '#' symbol), the goal here is to make the files easily readable with the same Python script.

Ideally, we would want `MJD, Band, Instrument, Magnitude, Error, Upper limit` in that order, but not all supernovae will have this info handy.

Here's an example file for SN1937A:

```Python
# 1937PASP...49..204Z
# JD Band Magnitude Instrument "Upper limit"
2428521 mp 17.5 "18-inch Schmidt" true
2428524 mp 17.5 "18-inch Schmidt" true
2428581 mp 17.5 "18-inch Schmidt" false
2428599 mp 17.5 "18-inch Schmidt" false
2428600 mp 17.5 "18-inch Schmidt" false
2428635 mp 17.5 "18-inch Schmidt" false
2428636 mp 17.5 "18-inch Schmidt" false
2428664 mp 17.5 "18-inch Schmidt" true
2428667 mp 17.5 "18-inch Schmidt" false
