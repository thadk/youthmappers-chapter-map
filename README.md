This repository holds the source code for http://youthmappers.org/chapters main version that uses Mapbox GL.js to display content from a Google Sheet, with particular columns.

To control the chapters shown, request access to the <a href="https://docs.google.com/spreadsheets/d/13yswnN49P0dsO5BS2FJYaVUIjsnuWbzA3UxvhcLUsYI">YouthMappers Google Sheet</a>.

<img src="https://user-images.githubusercontent.com/283343/31572336-c89e2784-b071-11e7-8f9e-c8939732e291.png" width="500"/>

It can be live-edited using <a href="http://blockbuilder.org/thadk/9ca729c0f54dd0dc8ce338feaf2d4bf8">BlockBuilder.org</a> once forked.

## Enabling Cross Origin requests to Google Sheets CSV
It relies on Amazon Web Services API Gateway `resource` to Google Sheets set up as shown below to download the CSV and share it onward as an API (avoid its proxy feature). It should be deployed to a `stage`:
<img src="https://user-images.githubusercontent.com/283343/31572279-2ccf4762-b070-11e7-88db-09820032a502.png" width="700">
Where the HTTP URL for the spreadsheet to use is: GET https://docs.google.com/spreadsheets/d/13yswnN49P0dsO5BS2FJYaVUIjsnuWbzA3UxvhcLUsYI/export?format=csv&amp;id=13yswnN49P0dsO5BS2FJYaVUIjsnuWbzA3UxvhcLUsYI

* Wherever possible, change `application/json` to `text/csv`.
* Ensure  Access-Control-Allow-Origin is set for the "Integration Response">`Header Mappings` section.

* Also use the <a href="http://docs.aws.amazon.com/apigateway/latest/developerguide/how-to-cors.html#how-to-cors-console">"Enable CORS"</a> action.


## Fallback version for substandard WebGL browsers
The fallback version of the site that uses basic Mapbox.js is at: https://gist.github.com/thadk/be6de2478c8aae7656a582895de8ff08
A version of this on Wix is hardlinked to by the application and displayed when e.g. there are no graphics drivers installed in Windows and the user is on Chrome.

## Template for schools
The HTML template shown for each school is in the templatize() function.

## Updating Wix
Select-All in the index.html and paste into the iframe embed on Wix to install a new version. Mapbox GL acts differently in an iframe on mobile than it does running normally on this staging area server with BlockBuilder or Bl.ocks.org.

### External javascript
There are 2 small javascript files which are referenced by the index.html and hosted from this repository using rawgit.com -- including `util.js` and  `csv2json.js` . These could be brought inline to the `index.html` if needed or re-hosted in a new repository if they need to be modified.

### Raven error tracking.
There is a raven tracking script which logs errors such as WebGL failures.
