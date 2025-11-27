findNonSearchablePDFS.sh
 Search a directory of PDFs for searchable text and use OCR tools to make it searchable.
 
 To find and convert non PDFs that are scanned and not text-searchable, see if they
 have fonts. If the pdffont program returns an error code, then run the ocr tool to
 create a searchable pdf doc
 If you arent sure of where bash can be found for line 1 just use $which bash
