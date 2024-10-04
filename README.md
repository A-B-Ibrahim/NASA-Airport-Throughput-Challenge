# NASA-Airport-Throughput-Challenge
A repository for all work related to Team Pathfinders work on the NASA Airport Throughput Challenged hosted by bitgrit. The overarching goal is to create a real-time regression model capable of predicting the number of arriving flights within the next 3 hours.

## File Extract (Optional)
*This section refers to the "Bitgrit File Extract" Notebook.*
Is used to automatically extract files from the zip folders they were downloaded in a put them into a new directory. This processes can be done manually but this notebook allows for it to be done automatically (assuming you are using the expected format). It is expected that for each type of data (FUSAR, CWAM, METAR, and TAF) that you put all of their zip files into a specified [unzipped] folder. You will use the pathway to that specified folder and a pathway to the end destination folder in the notebook. Below is the expected nesting of the directories starting from the specified folder (The zip dir are exactly as downloaded for the challenge). This notebook is assuming you are using windows OS - there is a line in the notebook marked #can change to "elif '_MACOSX' not in zip_info.filename:" if running on MAC" that you can change if you are using MAC. 

    Expected CWAM pathway:
        non-zipped DIR (CWAM_pathway)
        -zip dir 1 (download from bitgrit challenge)
            --_MACOSX
            --Dir with YYMMDD_YYMMDD name representing the time window it refers to
                ---Dir with MM name representing the month it refers to no. 1
                    ----Dir with DD name representing the day it refers to no. 1
                        -----Dir with full datatime of forecast name no. 1
                            ------.bz2 file with data for datetime
                            
                        -----Dir with full datetime of forecast name no. 2
                        -----Dir with full datetime of forecast name etc.
                    ----Dir with DD name no. 2
                    ----Dir with DD name etc.
                ---Dir with MM name no. 2
                ---Dir with MM name etc.
                ---.DS_Store
        -zip dir 2 (download from bitgrit challenge)
        -zip dir 3 (download from bitgrit challenge)
        -zip dir etc. (download from bitgrit challenge)



    Expected FUSAR pathway:
        non-zipped DIR (FUSAR_pathway)
        -zip dir 1 (download from bitgrit challenge)
            --_MACOSX
            --Dir with Airport ICAO as name
                ---.csv file of fusar data no. 1
                ---.csv file of fusar data no. 2
                ---.csv file of fusar data etc.
                
                ---.DS_Store
        -zip dir 2 (download from bitgrit challenge)
        -zip dir 3 (download from bitgrit challenge)
        -zip dir etc. (download from bitgrit challenge)



    Expected METAR pathway:
        non-zipped DIR (METAR_pathway)
        -zip dir (download from bitgrit challenge)
            --nested zip dir no. 1
                ---_MACOSX
                ---Dir named METAR_train_part_[#]
                    ---.txt file with METAR data for a timestamp no. 1
                    ---.txt file with METAR data for a timestamp no. 2
                    ---.txt file with METAR data for a timestamp etc.
                
            --nested zip dir no. 2
            --nested zip dir etc.



    Expected TAF pathway:
        non-zipped DIR (TAF_pathway)
        -zipped dir (download from bitgrit challenge)
            --_MACOSX
            --dir named TAF_train
                ---.txt file of TAF data for a timestamp no. 1
                ---.txt file of TAF data for a timestamp no. 2
                ---.txt file of TAF data for a timestamp no. etc.

The end result of this notebook is having all the files extracted from there zipped directories and placed into an unzipped directory out-of-place (not nested within other directories). This is optional as it is possible to simply manually move of the data into desired unzipped directories.

## Dataset Organization (WIP)
*This section refers to the "Dataset Organization" Notebook.*
This notebook is used to both join the different types of data files together (the different FUSAR CSVs) as well as split the data into 4 hour blocks as this is what will be used for our model. This blocks will be transformed so that all information within the block is relative to there 'start-time'. Ex. 1500 in a block that started at 1300 will be represented as 2 hours. These blocks will then be merged into one csv file that is used for future steps.
