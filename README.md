# Emergency-Food-Security-Fund-project

### Introduction

One of the most popular and commonly used file formats is Portable Document Format, or
PDF, which has the capability to store a plethora of crucial information for organizations,
businesses, and institutions. In today's rapidly evolving digital economy, PDFs are becoming
a sustainable alternative to paper, allowing users to share, print, and view files across different
platforms. Despite their reliability for storing and formatting data, it remains challenging to
scrape, parse, and extract data from PDF files as they are versatile. In our project, we are
dealing with semi-structured data that doesn't transform accurately into columns or rows, due
to the nature of the pdf data files.

This project aims to analyze the Emergency Food Security Fund (EFSF) data made available
during the pandemic by the Canadian Federal Government. The EFSF was announced in 2020
to aid local food organizations with nearly $100 million in funds to deal with the food crisis
that arose amidst the COVID-19 pandemic. Food banks were unable to deal with the huge
demand that arose leading to food insecurity for numerous Canadians to eat nutritious food.
Agriculture and Agri-Food Canada partnered with 6 national organizations namely Salvation
Army, Breakfast Club of Canada, Second Harvest, la Tablee des Chefs, Community Food
Centres Canada and Food Banks Canada. These organizations funded a total of 3038 projects
including the purchase of fridges, food storage units, and delivery services partnering with community
centers, local churches, food banks and other charitable organizations. 20% of local partners
were also surveyed to understand the perspective of the underlying organization. The shared
information was analyzed to create performance reports and program results to report
to the Parliament.

The key objective of the project is to extract these valuable data points from the available
unstructured PDFs and give the researchers at the University of Toronto, the required data in an
efficient and reliable manner into Comma separated values (CSV) spreadsheets.

### Model Development

To parse the PDFs, we use open-source OCR (Optical Character Recognition) engines and
Python as the programming language of choice. After exhaustive testing, optimal OCR engines
were determined as EasyOCR and Tesseract with OpenCV aiding for image processing
techniques. The other packages that were considered were PaddleOCR, pyPD2, PDFQuery,
Excalibur and PDFminer were not able to parse the text due to the nature of the data file as
the document is image-based rather than text-based for parsing. Tabula, another pdf parser
package that is used in Python was able to parse some of the data using inbuilt functions,
however, due to the image-based nature of the file, the tabula functions were unable to parse
some of the records. The tabula functions were modified using custom code to run in batches
of code, however, it was unable to parse all the information.


### Extraction process

During the data extraction process, the files were divided into three main subcategories due to the
same column headers on alternative pages. For File A, the data for pages until 1544 and data for
pages from 1545 until the end of the file are segmented into two subsets as they follow a particular
pattern of odd and even pages making up a single whole page. For File B, data for the first 45 pages
and data for pages 46 until the end of the file are segmented. Each page of the PDF file was
converted into an image using the PDF2Image library. To ensure sharper text for processing, the OpenCV
library was used to enhance the quality of the individual images by pre-processing them to
grayscale, and all images were normalized to a constant aspect ratio.

The widths of the column headers remained the same across each segment and were computed for
extraction. The heights, however, varied as the number of data records vary across each page. The
varying heights are computed by taking the height of the first row and the difference in height
between each row until it reaches the end of the page. While Pytesseract was used to get the data
from the image and convert it to an editable text format, EasyOCR was found to be the best tool
for reading the data. The masked Personal Identifiable Information (PII) data and empty rows are
stored as null values. The page numbers are also added at the end to indicate the page of the PDF
file from which it was extracted and the file. The resulting data array is stored in a CSV file for
further analysis.

The final output after parsing all the raw text is stored in an array using high-performance
cloud computing resources. A CSV writeback of the array is performed to store the information
into spreadsheets that allow the researchers to use the data immediately using MS Excel without
the need of installing any external tools or setting up databases. The spreadsheets are
uploaded to perform text mining operations, exploratory data analysis, descriptive analysis,
and sentiment analysis to gain data-driven insights for the researchers. There are a total of
10488 records in File A and 3513 records in File B that were extracted.
