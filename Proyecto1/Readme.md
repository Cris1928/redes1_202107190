#### Universidad de San Carlos de Guatemala
#### Facultad de Ingeniería
#### Redes de Computadoras 1
#### Primer Semestre de 2024

|Nombre  | Carnet | 
|------------- | -------------|
|Jorge Sebastian Zamora Polanco  | 202002591|
| Cristian Daniel Gomez Escobar |202107190 |

## Manual Tecnico

# Proyecto 1

## Resumen de direcciones IP y VLAN
  La empresa posee 4 departamentos con diferente VLAN que serian Contabilidad, Secretaria, Recursos
Humanos(RRHH) e Informática (IT). 
  
  |Departamento  | VLAN  |  ID de red | 
  |------------- | -------------| ------------|
  | Contabilidad | 11  | 192.168.11.10/12 |
  | Secretaria | 21 | 192.168.21.10/12 |
  | RRHH | 31 | 192.168.31.10/13 |
  | IT | 41 | 192.168.41.10/13 |

  ## Capturas de la implementación de las topologías.

- Cento de Administracion

   [![Topologia1.jpg](https://i.postimg.cc/PfSR26x1/Topologia1.jpg)](https://postimg.cc/kDts5vW5)

- Backbone

  [![Topologia2.jpg](https://i.postimg.cc/fLb5S9dY/Topologia2.jpg)](https://postimg.cc/3yP2PWnw)


- Área de trabajo
 
  [![Topologia3.jpg](https://i.postimg.cc/HsLcGtgw/Topologia3.jpg)](https://postimg.cc/G9ZhGG9t)

## Comandos Usados

  - Comandos de inicio
  Ingresamos comandos para desactivar la función de búsqueda de dominio DNS y cambiale el nombre a nuestro switch

    ```
    Swtich(config# no ip domain-lookup
    Switch(config)# hostname SW1
    ```

  - Declarar el switch raiz 
   Declaramos el switch que sera el raiz en nuestra red, significa que tendra un prioridad mas baja al resto
  
    ```
    SW1# configure terminal
    SW1(config)# spanning-tree vlan 1-4094 root primary
    ```
  - Swtich VTP modo servidor
  Configuración VTP en modo servidor en el switch servidor.
   
    ```
    SW1(config)# vtp version 2
    SW1(config)# vtp mode server
    SW1(config)# vtp domain P5
    SW1(config)# vtp password P5
    ```
  - Declarar Vlan's
  Creamos y definimos las Vlan's que usaremos en nuestra red
   
    ```
    SW1(config)# vlan 11
    SW1(config-vlan)# name CONTABILIDAD
    SW1(config-vlan)# exit
      
    SW1(config)# vlan 21
    SW1(config-vlan)# name SECRETARIA
    SW1(config-vlan)# exit
      
    SW1(config)# vlan 31
    SW1(config-vlan)# name RRHH
    SW1(config-vlan)# exit
      
    SW1(config)# vlan 41
    SW1(config-vlan)# name IT
    SW1(config-vlan)# exit

    ```
  - Vlan root
  Se configuran las VLAN para que pertenezcan al Root Bridge.
   
    ```
    SW1(config)# spanning-tree vlan 1 root primary
    SW1(config)# spanning-tree vlan 11 root primary
    SW1(config)# spanning-tree vlan 21 root primary
    SW1(config)# spanning-tree vlan 31 root primary
    SW1(config)# spanning-tree vlan 41 root primary
    ```
  - Interfaz modo truncal
  Configuramos las interfaces que se conectan con otros switichs en modo truncal, pasamos las Vlan que nos interesan
   
    ```
    SW1(config)# interface fa0/1
    SW1(config-if)# switchport trunk encapsulation dot1q
    SW1(config-if)# switchport mode trunk
    SW1(config-if)#switchport trunk allowed vlan 1, 11,21 ,31, 41 ,1002-1005
    ```
  - Switch VTP modo cliente
  Configuramos el switch en modo cliente en el mismo dominio en el que estan nuestras Vlan's

    ```
    SW2(config)# vtp version 2
    SW2(config)# vtp mode client
    SW2(config)# vtp domain P5
    SW2(config)# vtp password P5
    ```

  - Interfaz modo access
  Configuramos nuestra interfaz con dispositivos finales y le asignamos una Vlan especifica

    ```
    SW2(config)# interface FastEthernet 0/1
    SW2(config-if)# switchport mode access
    SW2(config-if)# switchport access vlan <número-de-VLAN>
    ```
  - Switch VTP modo Transparente
  Configuramos el switch en modo transparente

    ```
    SW9(config)# vtp version 2
    SW9(config)# vtp mode transparent
    SW9(config)# vtp domain P5
    SW9(config)# vtp password P5
    ```

  ## Ping entre hosts

   - Ping entre CONTABILIDAD2 a CONTABILIDAD1

  [![Ping11.jpg](https://i.postimg.cc/4NW9vYTw/Ping11.jpg)](https://postimg.cc/9rq0CF0q)

  - Ping entre RRHH1 a RRHH2

  [![Ping2.jpg](https://i.postimg.cc/HnMCYZCj/Ping2.jpg)](https://postimg.cc/MfzLtYH8)

  

  
