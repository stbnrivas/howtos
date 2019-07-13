# wget

get \
     --recursive \
     --no-clobber \
     --page-requisites \
     --html-extension \
     --convert-links \
     --restrict-file-names=windows \
     --domains website.org \
     --no-parent \
         www.website.org/tutorials/html/





DOMAIN = website.org
URL = www.website.org/tutorials/html/

get --recursive --no-clobber --page-requisites --html-extension --convert-links --restrict-file-names=windows --domains $DOMAIN --no-parent $URL 