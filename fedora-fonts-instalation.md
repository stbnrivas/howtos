Installing with font viewer

You can preview and install font files using the gnome-font-viewer utility. Once you installed it, double clicking font files will open it in this utility. This utility can be installed using:

yum install -y gnome-font-viewer

Remember, this utility will install fonts in the user's font directory (~/.fonts). This means that the font will be available only for the user who installed it.




    Manual installation

        User specific installation

        Login as the user for which you want to install the font. Then open the .fonts directory - create one if it doesn't exists. Remember, it will be on your home directory and will be hidden by default. You can show or hide hidden directories in nautilus with Ctrl+H. Copy the font files to this .fonts directory. Now, open a terminal and type the following command to make the users’ accounts aware of the fonts.

        fc-cache -v

        System wide installation

        The system wide fonts are installed in the directory /usr/share/fonts. Create a directory there to hold your font collection, and copy the fonts to that newly created directory. Then run fc-cache -v to make the system aware of the newly installed fonts. You need root permission to make changes in /usr/share/fonts. You can use sudo or su - for that

        ### using sudo ###
        sudo nautilus /usr/share/fonts
        ### this will open nautilus as root. create directory and copy fonts. then
        sudo fc-cache -v

        ### using su - ###
        su -
        nautilus /usr/share/fonts
        ### this will open nautilus as root. create directory and copy fonts. then
        fc-cache -v

    fc-cache scans the font directories on the system and builds font information cache files for applications using fontconfig for their font handling. To force the re-generation of apparently up-to-date cache files, overriding the timestamp checking, you can issue the -f flag.

    fc-cache -f -v

gotcha: With some applications like Scribus and The Gimp, the more fonts you add, the longer it will take for the applications to start up. So if your collection is reaching into the thousands, expect those applications to take a moment to start.
