# Invoice pdf creation tool :ledger: :pound:
Simple node script that takes json input and creates an invoice pdf output using the passed json and an html/angular template

## Instructions
Clone the repo to where ever you like, cd into the 'invoiceCreation' directory then run npm install to install the node dependancies.

After that you'll probably want to change some of the defaults like the company address, logo and bank details. You can find most of these in the 'globalModel' object in the following file: invoiceCreation/ngApp/scripts/invoiceApp.js. You don't need to edit the 'model' object as that data is passed through as a parameter when calling the script. To change the logo you'll want to edit invoiceCreation/invoiceAngular.html, search for 'invoiceLogo.png' and replace it with anything you like.

To run the script you need to pass through 2 parameters. The first parameter is the work data for the invoice you want to create, the second parameter is the location (including the filename) where you would like the tool to save the output to.

There are 2 options when it comes to passing through the work data to the tool, the first one is to pass through the path to a json file like so:

``` shell
node createInvoice.js ~/Desktop/invoiceData_01_01_16.json ~/Desktop/invoiceOutput.pdf
```

The json file should have the following schema:

```json
{
	"purchaseOrderId": 1234,
	"invoiceNumber": 1,
	"invoiceDate": "03/01/16",
	"invoiceDescription": "Work I did for this company",
	"nameAndEmail": "John Doe, john.doe@somewhere.com",
	"workBreakDown": [
		{
			"date": "01/01/16",
			"timeWorkedInHours": 8,
			"dayRate": 600
		},
		{
			"date": "02/01/16",
			"timeWorkedInHours": 8,
			"dayRate": 675.5
		}
	]
}
```

Instead of passing through a path to a json file you can alternativley pass through the same json as a string like so:
``` shell
node createInvoice.js '{"purchaseOrderId":1234,"invoiceNumber":1,"invoiceDate":"03/01/16","invoiceDescription":"Work I did for this company","nameAndEmail":"John Doe, john.doe@somewhere.com","workBreakDown":[{"date":"01/01/16","timeWorkedInHours":8,"dayRate":600},{"date":"02/01/16","timeWorkedInHours":8,"dayRate":675.5}]}' ~/Desktop/invoiceOutput.pdf
```

Finally I've added an alias to my .bashrc file so that I don't have to reference the location of the createInvoice.js file when I want to run it, this is up to you though, heres an example of my alias:

```
#invoice creation tool alias
alias createInvoice='node ~/path/to/createInvoice.js'
```

Then you can run the script like this:

``` shell
createInvoice ~/Desktop/invoiceData_01_01_16.json ~/Desktop/invoiceOutput.pdf
```