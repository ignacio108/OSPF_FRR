# OSPF_FRR
Virtual Lab using VNX( Virtual Networks over linuX)  to test the security of OSPFv2 and OSPFv3

# Escenario de pruebas OSPF-FRR (3/2025)


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