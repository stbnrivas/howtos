# rsync

    rsync -v file_input file_output
    rsync -vv file_input file_output
    rsync -vvv file_input file_output

## importantance of slash at end of folder name

without slash means /path/foo the directory foo
with slash means /path/foo/ all contains inside folder foo

    rsync -av folderInput/ folderOutput/
    rsync -av folderInput/ folderOutput

    rsync -av folderInput folderOutput/
    rsync -av folderInput folderOutput

## to delete files that was delete at input but now are in output

    rsync -av --delete folderInput/ folderOutput

    # to test commands params without delete use:
    -n / --dry-run

## incrementals backup option

    -b / --backup / --backup-dir=DIR

    #! NEVER USE RELATIVE PATH WITH THIS OPTION,
    #! BECAUSE DELETE ALL IF SPECIFY BAD THE DIRECTORY FOLDER

    rsync -avb --delete --backup-dir=$PWD/backup-$(date+%y%m%d) folderInput/ folderOutput/

## including and excluding files to backup

    --exclude=PATTERN       exclude files matching PATTERN
    --exclude-from=FILE     read exclude patterns from FILE
    --include=PATTERN       don't exclude files matching PATTERN
    --include-from=FILE     read include patterns from FILE
    --files-from=FILE       read list of source-file names from FILE

### examples of file text for specify directory to backup

    list_dirs_backup.txt:
    + */
    + /var/www/**
    + /var/log/**
    - *

    rsync -av --delete --prune-empty-dirs --include-from=list_dirs_backup.txt / /mnt/disco/Backup/


    list_dirs_backup.txt:
    + /var/
    + /var/www/
    + /var/log/
    + /var/www/**
    + /var/log/**
    - *

    rsync -av --delete --include-from=list_dirs_backup.txt / /mnt/disco/Backup/


    + /var/
    + /var/www/***
    + /var/log/***
    - *
## rsync backup to remote machine

rsync -av --progress /media/storeHD/knowledge/ admin@192.168.1.115:/share/Books/computerScience/

rsync -av --progress /media/storeHD/Music/ admin@192.168.1.115:/share/music/




