# folding-score-checker
A script to run in real-time to track point differences as one is contributing to Stanford's Folding@Home project

Author: Kyle Belouin (kyle.belouin@gmail.com)

Requires:
* Bash or zsh
* jq
* Internet connection

![Screenshot](https://user-images.githubusercontent.com/39029459/186545133-ad4b7b2b-aaf6-4884-954f-1d496d611c2b.png)

How to run:

To use the program, you must provide two parameters, your delay (in seconds) for a pause in between checks, and your Folding@Home user ID respectively.

For example: ./run 3600 867530

Design:

The script is intended to be left running for long periods of time, so that you can track how many points you accrue over particular lengths of time. Analysis of the data is manual, and can be done by parsing the file `log.txt`.

For difference calculations, two 'origin' data points need to be defined.

First is a lifetime origin. This origin is determined automatically upon the first run of the program, creating a number in a file called `.origin`. The program will check for this file, and if it is absent, will define it with the value of your current user score. This file is not expected to change over time, it is useful because you can track your point growth over time, from the first time you use the program to the present. HINT: if you want to 'reset' this origin, simply remove .origin (rm .origin) from the project root folder.

Second, another origin is set based on the current point value at the start of a particular program instance, it will track difference for a particular current run only.

Attribution:
This project relies on Stanford's FoldingAtHome API, which they have made publicly available. API requests are simple cURL GETs and do not require any authentication. The object returned is JSON and is readily formatted for use with `jq`.

Source URL being parsed: https://api2.foldingathome.org/uid/$UserID/ where $UserID is your user ID. Because this is an external resource, this structure is subject to change (but it is an API that many people rely on, it should be safe from erroneous changes).

