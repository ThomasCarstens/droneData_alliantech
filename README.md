# drone_data_alliantech
Drone data and other data collected at Alliantech.

* LOGGING: https://docs.px4.io/master/en/dev_log/logging.html 
* EXECUTABLES: https://docs.px4.io/master/en/modules/hello_sky.html 
* CIRCUIT SUR DRONE: https://docs.px4.io/master/en/flight_controller/pixhawk4.html#serial-port-mapping 
* PX4 DEVELOPER ENVIRONMENT: https://docs.px4.io/master/en/dev_setup/dev_env.html 
* DRONE DATA, ETAT DE L’ART, BOITIERS, RAPPORTS ET SUPPORTS IMPRIMES: Google Drive partage avec Alliantech.

# LES COMMANDES UTILES LORS D’UN VOL
⚠️ Requires: linux,github, docker.

## POUR LANCER L’ACQUISITION DE DONNEES
⚠️ Requires: DAQ Connected to D11 PIN || OPEN NSH CONSOLE
### RESET PIN (0) AT STARTUP, THEN POWER UP DAQ

  nsh> px4_slice_disconnect
### SET PIN (1) TO START LOGGING

  nsh> px4_slice_disconnect

The data-logging activation file was coded in C++, and compiled into an executable via the MAVLink protocol. 
During operation, it simply toggles a pin (FMU Channel 6), which can then be detected by the data acquisition system in order to begin and end the logging. 
The executables are named as above.


# LES COMMANDES UTILES POUR ORGANISER LES LOGS / GROUNDSTATION

## POUR COMPILER UNE FONCTIONNALITÉ MAVLINK (EG. EXTRA LOG) 
⚠️ Requires: mavlink repo from github (compiled)+docker setup

  sudo docker run --rm -v ${PWD}:/project/source -v ${PWD}/build:/project/build qgc-linux-docker

## POUR CONVERTIR UN LOG PIXHAWK EN CSV  

⚠️ Requires: ulog2csv lib
  ulog2csv log_0_2021-8-10-04-37-02.ulg

## POUR FLASHER DU FIRMWARE SUR LE DRONE
⚠️ Requires: PX4-Autopilot from github (compiled)

  cd ../PX4-Autopilot/
  make px4_fmu-v5_default upload

## POUR LANCER LA VERSION DEV DE QGC
⚠️ Requires: qgc repo from github (compiled)

  cd Documents/qgroundcontrol/build/staging
  ./qgroundcontrol

# LES COMMANDES UTILES POUR LA LOCALIZATION EXTERNE

## POUR EXECUTER UN ROSBAG

  rosbag play xr1.bag -l -a

## POUR EXTRAIRE UN CSV D’UN ROSBAG

  rostopic echo -b xr1.bag -p /tf >> xr1.csv

