# droneData_alliantech
Documentation of resources used during Drone Internship.

# RESOURCES AND LINKS

* DRONE DATA, ETAT DE L’ART, BOITIERS, RAPPORTS ET SUPPORTS IMPRIMES: 
> Google Drive partage avec Alliantech.

* PX4 DEVELOPER ENVIRONMENT 
> https://docs.px4.io/master/en/dev_setup/dev_env.html 
> ⚠️ Requires: linux,github, docker.

* LOGGING:
> https://docs.px4.io/master/en/dev_log/logging.html 

* EXECUTABLES: 
> https://docs.px4.io/master/en/modules/hello_sky.html 
> The data-logging activation file was coded in C++, and compiled into an executable via the MAVLink protocol. 
> During operation, it simply toggles a pin (FMU Channel 6), which can then be detected by the data acquisition system in order to begin and end the logging. 

* CIRCUIT SUR DRONE: 
> https://docs.px4.io/master/en/flight_controller/pixhawk4.html#serial-port-mapping 


# LES COMMANDES UTILES LORS D’UN VOL


## Pour lancer l'acquisition de donnees
OPEN NSH CONSOLE. ⚠️ Requires: DAQ Connected to D11 PIN 

### RESET PIN (0) AT STARTUP, THEN POWER UP DAQ
    nsh> px4_slice_disconnect
### SET PIN (1) TO START LOGGING
    nsh> px4_slice_disconnect

# LES COMMANDES UTILES POUR ORGANISER LES LOGS / GROUNDSTATION

## Pour compiler la librairie mavlink (add logs, ui...)
⚠️ Requires: mavlink repo from github (compiled)+docker setup

    sudo docker run --rm -v ${PWD}:/project/source -v ${PWD}/build:/project/build qgc-linux-docker

## Pour convertir un log de la Pixhawk (.ulog) en .csv 

⚠️ Requires: ulog2csv lib

    ulog2csv log_0_2021-8-10-04-37-02.ulg

## Pour flasher du firmware sur la Pixhawk 4
⚠️ Requires: PX4-Autopilot from github (compiled)

    cd ../PX4-Autopilot/
    make px4_fmu-v5_default upload

## Pour lancer la version dev de QGC
⚠️ Requires: qgc repo from github (compiled)

    cd Documents/qgroundcontrol/build/staging
    ./qgroundcontrol

# LES COMMANDES UTILES POUR LIRE LES LOGS ROS

## Pour executer un rosbag

    rosbag play xr1.bag -l -a

## Pour extraire un csv d'un rosbag
### One topic
    rostopic echo -b xr1.bag -p /tf >> xr1.csv
### All topics
    for topic in `rostopic list -b bagfile.bag` ; do rostopic echo -p -b bagfile.bag $topic >bagfile-${topic//\//_}.csv ; done

## Timers
https://roboticsbackend.com/how-to-use-a-ros-timer-in-python-to-publish-data-at-a-fixed-rate/
