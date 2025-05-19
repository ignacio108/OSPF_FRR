El script change.key permite automatizar el cambio de claves en el proceso de OSPF.

    Su objetivo principar el modificar la key_id del keychain actual para añadirle un tiempo maximo de uso y crear una nueva key dentro de la misma key_chain para sustituir a la anterior.


    La lógica del cambio de claves es la siguiente

    Key en uso(key_id):
                        desde           hasta
    accept lifetime     date-time       date+time
    send   lifetime     date-time       date+time

    Key nueva(key_id+1):
                        desde           hasta
    accept lifetime     date            infinite
    send   lifetime     date            infinite


    sudo python3 change_key.py --key [Nombre del Key-chain, Key_id en uso, Clave_nueva] --routername [nombres de los routers] --time {segundos}

El argumento key:

    Define el nombre de la key_chain en uso, el key_id que se está utilizando y la nueva clave que será utilizada junto con el algoritmo hmac-sha-256 para el trailer de OSPF.

El argumento routername

    Define el conjunto de routers que se verán afectados por este cambio

    -all (Modifica todos los routers del escenario ["rA","rB","rC","rD","rE"])

El argumento time

    Define el numero de segundos que se utilizará de intervalo, el tiempo minimo es 60 segundos, si introducimos un tiempo menor a 60 segundo se utilizará 60 segundos

Ejemplos:

    sudo python3 change_key.py --key 1 1 EVANGELION --routername all --time 10

    sudo python3 change_key.py --key 1 4 EVANGELION3 --routername rA rB --time 100


Camndos para comprobar que se ha cambiado las keys:

    show ip ospf interface {interface_name}

    show running-config