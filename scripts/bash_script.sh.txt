#!/bin/bash 
 
db="max30102.db" 
table="heart_rate_data" 
 
echo "---- WELCOME ----" 
 
while [ 1 ] 
do 
        echo "Please select any query by typing its sr. no." 
 
        echo " " 
        echo "1. View heart rate data (last 50 entries) of..." 
        echo "2. Calculate average heart rate of..." 
        echo "3. Compare average heart of users." 
        echo "4. View oxygen saturation (SpO2) data (last 50 entries) of..." 
        echo "5. Calculate average SpO2 of..." 
        echo "6. Compare average SpO2 of all users." 
 
        echo " " 
        echo -n "Enter sr. no. of query: " 
        read choice 
 
        if [ "$choice" = "" ];then echo "Value needed"; exit 1; fi 
 
        case $choice in 
                 1) 
                        echo " " 
                        echo "Select (complete the sentence):" 
                        echo "    1. ...a person (enter name)." 
                        echo "    2. ...all users." 
                        echo " " 
                        echo -n "Enter your choice: " 
                        read ans 
 
                        if [ "$ans" = 1 ]; then 
                                echo -n "Enter person name: " 
                                read person 
 
                                echo " " 
                                sqlite3 -header -column "$db" "SELECT timestamp, 
bpm FROM $table WHERE person='$person' ORDER BY id DESC LIMIT 50;" 
 
                        else 
                                echo "Displaying heart rate for all users." 
                                echo " " 
                                sqlite3 -header -column "$db" "SELECT timestamp, 
bpm FROM $table ORDER BY id DESC LIMIT 50;"
                        fi 
                        ;; 
 
                2) 
                        echo " " 
                        echo -n "Calculate average HR for: " 
                        read person 
 
                        echo " " 
                        sqlite3 -header -column "$db" "SELECT AVG(bpm) FROM $table 
WHERE person='$person';" 
                        ;; 
 
                3) 
                        echo " " 
                        echo "Comparing average heart rate of all users:" 
 
                        echo " " 
                        sqlite3 -header -column "$db" "SELECT person, AVG(bpm) FROM 
$table GROUP BY person;" 
                        ;; 
 
                4) 
                        echo " " 
                        echo "Select (complete the sentence):" 
                        echo "    1. ...a person (enter name)." 
                        echo "    2. ...all users." 
                        echo " " 
                        echo -n "Enter your choice: " 
                        read ans 
 
                        if [ "$ans" = 1 ]; then 
                                echo -n "Enter person name: " 
                                read person 
 
                                echo " " 
                                sqlite3 -header -column "$db" "SELECT timestamp, 
spo2 FROM $table WHERE person='$person' ORDER BY id DESC LIMIT 50;" 
 
                        else 
                                echo "Displaying SpO2 data for all users." 
 
                                echo " " 
                                sqlite3 -header -column "$db" "SELECT timestamp, 
person, spo2 FROM $table ORDER BY id DESC LIMIT 50;" 
 
                        fi 
                        ;;

                5) 
                        echo " " 
                        echo -n "Enter name of person: " 
                        read person 
 
                        echo " " 
                        sqlite3 -header -column "$db" "SELECT AVG(spo2) as 
Average_SpO2 FROM $table WHERE person='$person';" 
                        ;; 
 
                6) 
                        echo " " 
                        echo "Comparing average SpO2 of all users:" 
 
                        echo " " 
                        sqlite3 -header -column "$db" "SELECT person, AVG(spo2) as 
Average_SpO2 FROM $table GROUP BY person;" 
                        ;; 
 
     7) 
                        echo " " 
                        echo -n "Enter name of person: " 
                        read person 
 
                        echo " " 
                        sqlite3 -header -column "$db" "SELECT MAX(bpm) AS max_bpm, 
MIN(bpm) AS min_bpm, AVG(bpm) AS avg_bpm, MAX(spo2) AS max_spo2, MIN(spo2) AS 
min_spo2, avg(spo2) AS avg_spo2 FROM $table WHERE person=’$person’” 
       ;; 
 
                *) 
         echo 
                     echo "Invalid selection. Please enter a number between 1 
and 6." 
                  ;; 
 
        esac 
 
        echo " " 
        echo -n "Do you want to continue? (Y/n): " 
        read t_choice 
 
        if [ "$t_choice" = 'n' ]; then echo "Exiting program..."; exit 0; 
        else clear; fi; 
 
done