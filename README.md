# Citation.js QuickStatements plugin

This npm package is a plugin to citation.js
([see this article](https://peerj.com/articles/cs-214/)) that outputs bibliographic information
to [Wikidata QuickStatements](https://quickstatements.toolforge.org/). Some important points:

1. it does *not* (currently) check if the information is already in Wikidata
2. it only supports journals articles (at this moment)


## Install

```shell
npm install @citation-js/plugin-quickstatements
```

To run the below example, you also need to install a few other packages
(as they are currently not automatically pulled in, it seems):

```shell
npm install @citation-js/core @citation-js/plugin-pubmed @citation-js/plugin-doi @babel/register @babel/core
```


## Use

Install the plugin by `require`-ing it:

```js
require('@citation-js/plugin-quickstatements')
```

## Formats

Formats and other features added by this plugin.

### Input

The input is CSL generated by citation.js by any of its supported formats.
Here's an example for how to create QuickStatements for a PubMed Central
identifier:

```javascript
c = require('@citation-js/core')
require('@citation-js/plugin-pubmed')
require('@citation-js/plugin-doi')

require('@babel/register')
require('@citation-js/plugin-quickstatements')

c.Cite.async([
  '10.1186/s13321-019-0380-5',
  'pmid:14266813',
  'PMC6613236'
])
  .then(Cite =>
    console.log(Cite.format('quickstatements'))
  )
  .catch(console.error)
```

Or for book ISBN numbers:

```javascript
const c = require('@citation-js/core')
require('@citation-js/plugin-isbn')

require('@babel/register')
require('@citation-js/plugin-quickstatements')

c.Cite.async([
  '978-0956775016'
])
  .then(Cite =>
    console.log(Cite.format('quickstatements'))
  )
  .catch(console.error)
```

### Output

The output is [QuickStatements](https://www.wikidata.org/wiki/Help:QuickStatements) to be copied
into the [online webservice](https://tools.wmflabs.org/quickstatements/). The output
looks like:

```
	CREATE

	LAST	P31	Q13442814
	LAST	Len	"Journal of Cheminformatics, ORCID, and GitHub"
	LAST	P304	"44"
	LAST	P356	"10.1186/s13321-019-0365-4"
	LAST	P433	"1"
	LAST	P478	"11"
	LAST	P698	"31281945"
	LAST	P932	"PMC6613236"
	LAST	P1476	"Journal of Cheminformatics, ORCID, and GitHub"
	LAST	P577	"2019-07-08"
	LAST	P2093	"Egon Willighagen"	P1545	"1"	
	LAST	P2093	"Nina Jeliazkova"	P1545	"2"	
	LAST	P2093	"Rajarshi Guha"	P1545	"3"
```
