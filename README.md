# OSPF_FRR
Virtual Lab using VNX( Virtual Networks over linuX)  to test the security of OSPFv2 and OSPFv3

# Preparación del escenario

Es necesario descargar la imagen que utilizarán las instacias del escenario.

En el directorio de filesystems es necesario ejecutar los siguientes comandos:

OSPF_FRR/filesystems

sudo vnx_download_rootfs -r vnx_rootfs_lxc_ubuntu64-22.04-v025-vnxlab.tgz

sudo ln -s vnx_rootfs_lxc_ubuntu64-22.04-v025-vnxlab rootfs_lxc



# Escenario de pruebas OSPF-FRR 


OSPF con dos areas, un area 0 (backbone) con 3 routers interconectados con enlaces punto a punto.
Y otra area (area 1) con routers conectados con enlaces punto a multipunto.

Ambos tienen configurados ipv4 e ipv6.

DOS ESCENARIOS:

Escenario sin seguridad en las areas de OSPF:


sudo vnx -f frr-ospf-lan.xml -x loadra
sudo vnx -f frr-ospf-lan.xml -x loadrb
sudo vnx -f frr-ospf-lan.xml -x loadrc
sudo vnx -f frr-ospf-lan.xml -x loadrd
sudo vnx -f frr-ospf-lan.xml -x loadre

-----------------------------------------------------------------------------------------------------------
Escenario con seguridad (OSPF trailer):

Comando para cargar todas las configuraciones en los routers correspondientes:

sudo vnx -f frr-ospf-lan.xml -x load_keys



sudo vnx -f frr-ospf-lan.xml -x loadra_key
sudo vnx -f frr-ospf-lan.xml -x loadrb_key
sudo vnx -f frr-ospf-lan.xml -x loadrc_key
sudo vnx -f frr-ospf-lan.xml -x loadrd_key
sudo vnx -f frr-ospf-lan.xml -x loadre_key


-----------------------------------------------------------------------------------------------------------
POR DEFECTO CARGA EL ESCENARIO SIN AUTENTICACION EN OSPF.

FRR no permite el uso de IPSEC en OSPF, directamente no es posible configurar el comando en la consola.


-----------------------------------------------------------------------------------------------------------

Hosts:

rA-netA:	fd80:e42c:3ce3:a66a::1/64	10.7.1.1/24
rA-netA-B:	fd80:e42c:3ce3:a770::1/64	10.8.1.1/24
rA-netA-C:	fd80:e42c:3ce3:a770::2/64	10.8.1.2/24
hA:			fd80:e42c:3ce3:a66a::10/64	10.7.1.10/24
rB-netB:	fd80:e42c:3ce3:a66b::1/64	10.7.2.1/24
rB-netA-B:	fd80:e42c:3ce3:a770::3/64	10.8.1.3/24
rB-netB-C:	fd80:e42c:3ce3:a770::4/64	10.8.1.4/24
hb: 		fd80:e42c:3ce3:a66b::10/64	10.7.2.10/24
rC-netC:	fd80:e42c:3ce3:a66c::1/64	10.7.3.1/24
rC-netA-C:	fd80:e42c:3ce3:a770::5/64	10.8.1.5/24
rC-netB-C:	fd80:e42c:3ce3:a770::6/64	10.8.1.6/24
hc: 		fd80:e42c:3ce3:a66c::10/64	10.7.3.10/24
rD-netD:	fd80:e42c:3ce3:a66d::1/64	10.7.4.1/24
rD-netA:	fd80:e42c:3ce3:a66a::2/64	10.7.1.2/24
hd:			fd80:e42c:3ce3:a66d::10/64	10.7.4.10/24
rE-netE:	fd80:e42c:3ce3:a66e::1/64	10.7.5.1/24
rE-netA:	fd80:e42c:3ce3:a66a::3/64	10.7.1.3/24
he:			fd80:e42c:3ce3:a66e::10/64	10.7.5.10/24