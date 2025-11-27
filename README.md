 #findNonSearchablePDFS.sh
 #search a directory of PDFs for searchable text and use OCR tools to make it searchable
 #!/usr/bin/bash
# To find and convert non PDFs that are scanned and not text-searchable, see if they
# have fonts. If the pdffont program returns an error code, then run the ocr tool to
# create a searchable pdf doc
# If you arent sure of where bash can be found for line 1 just use $which bash
saveIFS=$IFS
IFS=$(echo -en "\n\b")
# find pdfs to scan
FilesToCheck=$(find `pwd` -maxdepth 2 -name "*.pdf")
counter=0
for i in $FilesToCheck
do
   # debugging   print them all .....
   echo $i
   # check for fonts which means it contains text. err code means no fonts and no text
   errCheck=$(pdffonts ${i} 2>&1 | tail -1)
   err="$?"
   #or just check for $? being zero or numeric maybe
   if [[ $errCheck =~ ^- ]]
   then
       echo ">>>>>>> BAD DOC:  No searchable fonts found. Needs OCR Converted. $i   "
       #make a backup of original  just in case
       cp $i badpdfs
       #convert it to be searchable
       pdfsandwich $i -o out.pdf
   else
       #printf "       GOOD DOC : $err $i \n"
       counter=$((counter+1))
       #mv $i goodpdfs
   fi
done

IFS=$saveIFS
