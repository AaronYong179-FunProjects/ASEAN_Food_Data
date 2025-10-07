# ASEAN Food Data

## Data

**ASEAN Food Composition Database (FCD), 2014**

_Source_

The relevant document can be found [here](https://inmu.mahidol.ac.th/aseanfoods/doc/OnlineASEAN_FCD_V1_2014.pdf). This is the only source I could find, and is also the only one linked by the [Food and Agriculture Organization of the United Nations](https://www.fao.org/infoods/infoods/tables-and-databases/asia/en/).

_Extraction_

The data is embedded in quite a wonky table. Known pdf table extractors (`tabula-py` and `camelot`) did not work very well. I had to resort to extracting all text as markdown with `pymupdf4llm` and then process the data further with Python. 

Note that the following columns are ommited:
- "Origin", as I could not find any mapping for the codes used in the document.
- "Alternate name", as the Thai scripts were not fully captured by `utf-8`. 
- "DEN" (density), as I did not think this relevant information.

_Further Notes_

The data is formatted as a `.csv` file for easy programmatic access. However, downstream preprocessing is absolutely required, as the nutritional values are not all numerical. 
- For example, some values are enclosed within parentheses. These only affect the columns ENERC (energy) and CHOAVLDF (carbohydrates). I believe that the parentheses indicate that these values are derived from other nutritional components (p. 27, xxiii, ASEAN FCD 2014).
- Some values might also be indicated as "0p", which stands for presumed zero (p. 27, xxiii, ASEAN FCD 2014)