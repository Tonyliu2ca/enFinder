#!/bin/bash

readonly LOG_ERROR=1
readonly LOG_WARNING=3
readonly LOG_INFO=5

LOGLEVEL=5
# --------------------------------------------------------------------
# Input:
#   $1: log level
#   $2: category
#   #3: log string
# --------------------------------------------------------------------
myLoger()
{
	[ $1 -le $LOGLEVEL ] && logger -i "   $2: $3"
}

# --------------------------------------------------------------------
# Replace 访达 to Finder in place a PLIST file
# Input:
#   $1: the file
# --------------------------------------------------------------------
function enFinder()
{
	plutil -lint -s "$1"
	if [ $? -eq 0 ]; then
		myLoger $LOG_INFO "enFinder(info)" "1. is PLIST: [$1]"
		ISBINARY=$(head -n 1 "$1" | grep "bplist")
		if [ "$ISBINARY" != "" ]; then
			myLoger $LOG_INFO "enFinder(info)" "2. is binary format."
			tmpfile=$(/usr/bin/mktemp /tmp/enFinder.XXXXXXXX)
			plutil -convert xml1 "$1" -o "$tmpfile"
			myLoger $LOG_INFO "enFinder(info)" "3. convert to XML format."
			sed -i "" "s/访达/Finder/g" "$tmpfile"
			myLoger $LOG_INFO "enFinder(info)" "4. change to Finder."
			plutil -convert binary1 "$tmpfile" -o "$1"
			myLoger $LOG_INFO "enFinder(info)" "5. convert back to binary."
			rm "$tmpfile"
		else
			myLoger $LOG_INFO "enFinder(info)" "2. is XML format."
			sed -i "" "s/访达/Finder/g" "$1"
			myLoger $LOG_INFO "enFinder(info)" "3. change to Finder."
		fi
	else
		myLoger $LOG_INFO "enFinder(info)" "1. not PLIST: [$1]"
	fi
}


# --------------------------------------------------------------------
# Process all files in a folder change to Finder
# Input:
#   $1: the folder
# --------------------------------------------------------------------
function pFilesInFolder()
{
	myLoger $LOG_INFO "pFilesInFolder(info)" "1. process path：$1"
	ALLFILES=$(ls "$1")
	for EACHFILE in $ALLFILES; do
		myLoger $LOG_INFO "pFilesInFolder(info)" "2. process：$EACHFILE"
		if [ ! -e "$1/${EACHFILE}.org" ]; then
			myLoger $LOG_INFO "pFilesInFolder(info)" "3. backup to ${EACHFILE}.org"
			cp "$1/${EACHFILE}" "$1/${EACHFILE}.org"
		else
			myLoger $LOG_INFO "pFilesInFolder(info)" "3. backup file exists ${EACHFILE}.org"
		fi
		enFinder "$1/${EACHFILE}"
	done
}


# --------------------------------------------------------------------
# Process all files in a folder change to 访达
# Input:
#   $1: the folder
# --------------------------------------------------------------------
function RestoreFolder()
{
	myLoger $LOG_INFO "RestoreFolder(info)" "1. process path：$1"
	ALLFILES=$(ls "$1")
	for EACHFILE in $ALLFILES; do
		myLoger $LOG_INFO "RestoreFolder(info)" "2. process：$EACHFILE"
		if [ -e "$1/${EACHFILE}.org" ]; then
			myLoger $LOG_INFO "RestoreFolder(info)" "3. restore from ${EACHFILE}.org"
			mv -f "$1/${EACHFILE}.org" "$1/${EACHFILE}" &>/dev/null
		else
			myLoger $LOG_INFO "RestoreFolder(info)" "3. backup file NOT exists ${EACHFILE}.org"
		fi
	done
}

myLoger $LOG_INFO "Main" "EnglishFinder: Start..."
if [ "$1" = "English" ]; then
	pFilesInFolder "/System/Library/CoreServices/Dock.app/Contents/Resources/zh_CN.lproj"
	pFilesInFolder "/System/Library/CoreServices/Finder.app/Contents/Resources/zh_CN.lproj"
elif [ "$1" = "Chinese" ]; then
	RestoreFolder "/System/Library/CoreServices/Dock.app/Contents/Resources/zh_CN.lproj"
	RestoreFolder "/System/Library/CoreServices/Finder.app/Contents/Resources/zh_CN.lproj"
else
	echo "Usage:"
	echo "   EnglishFinder [English|Chinese]"
	echo "Tony Liu, Copyright 2017"
	echo ""
fi
myLoger $LOG_INFO "Main" "EnglishFinder: Complete..."
