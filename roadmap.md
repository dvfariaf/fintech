# Extracting data from PDF

-	Tabula: 
	-	(pros)
		-	based on tabula and pandas!
		-	frequently maintained
		-	python and R bindings (https://github.com/chezou/tabula-py)
	-	(cons) 
		-	to be seen

## Regular account

### Format

-	Types of operations and format
		-	Generated transfers: Initiated by the account owner
				- External transfers:
						- Attributes: POUR / REF / MOTIF / CHEZ
				- Internal transfers:
						- Attributes: VERSEMENT PROGRAMME
		-	Received transfers: Received from a tier
				- Attributes: DE / MOTIF / REF / CHEZ
		-	Charge: amount taken by a tier (prelevement)
				- Attributes: DE / ID / REF / MANDAT / MOTIF: Numero de client: [0-9] - Numero de compte: [x0-9]
		-	Cash withdrawals: from ATMs
		-	Bank fees: i.e. from international expenses
				-	International fee: 
					-	Attributes:
				- 	Product fee:
					-	Attributes:
		-	Card debit: automatic payment of debit/credit card
		-	Checks:
				- Attributes: NONE
		-	Month start status: Description of status at month start (i.e. "*** SOLDE AU 31/03/2017 + 2.691,38 ***")
				- Attributes		
		-	Interests: 
			-Negative: interest from being negative on main account

			
-	TODO:
	* Develop unit testing. Hint: use the development files to check
	* pay special attention to guessed pages (what about the header?!!)
	* review that the cleaning is OK
	* that all the lines were correctly imported
	* writ somme check-ups and unit testing: # of columns, unread pages (if last=OK)...
	* clean the code a litle bit
	* then move to credit card...
	* Check known issues!
	
### Known Issues

-	On extracting data:
	-	[unsolved] when aggregating attributes in one line, some are uncorrectly concatenated. One attributes is in a multiple lines.
	-   [unsolved] the last few lines are sometimes not extracter
		-   __Solution__: Identify Zone: zhen not sure of the zone, then let Tabula Guess.
	-	[solved] 	Table reading doesn't identify well the area, missing the header.
		-	__Solution__: area defined correctly. NEEDS TABULA 0.9 and parameter Guess=True.
	-	[unsolved] ONLY APPLIES TO GUESSED PAGES. Header of the table not identified due to missing table formating in the PDF
		-	Consequences: unexistant column created due to information about the status of the account at the begginning of the period
		-	__Temporary Solution__: ignore this column by concatenating its results to the main operations detail
	-	[solved] Last row of the table, which states the total amount, is extracted
		-	__Solution__: filtered by using the operations detail (which is NaN)
	


	

### Next Steps
	-	Deal with the debit card PDF
	
	-	Put in DataBase (Docker)

	-	Integrate Excel Data recovered in the past

	-	Develop Dashboard with bokeh or something