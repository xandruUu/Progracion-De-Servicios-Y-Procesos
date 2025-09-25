## **Bloque 0: Historial**

0. Amplía el tamaño máximo del historial de la shell y configura que cada línea del historial muestre también la fecha y la hora.

```bash

export HISTSIZE=10000
export HISTFILESIZE=20000
export HISTTIMEFORMAT="%F %T "

history

 
```

1. Comprueba que ahora, al mostrar el historial, aparece la fecha y hora junto a los comandos ejecutados.

```bash
history
```

2. Configura estos cambios para que sean permantentes
```bash

#Abrir el archivo de configuración
nano ~/.bashrc

# Configuración del historial con fecha y hora
export HISTSIZE=1000
export HISTFILESIZE=20000
export HISTTIMEFORMAT="%F %T "

#Recargar la configuración sin cerrar sesión
source ~/.bashrc

```

---

## **Bloque 1: Gestión del sistema y el kernel**

1. Muestra toda la información de tu sistema operativo y kernel.
```bash

uname -a

```
    
2. Averigua únicamente la versión del kernel.
```bash

uname -r

```
    
3. Comprueba el espacio en disco disponible.
```bash

df -h

```
    
4. Calcula cuánto espacio ocupa la carpeta `/etc`.
```bash

du -sh /etc

# etc --> Carpeta donde se almacenan las configuraciones del sistema.

```
    
5. Consulta la memoria RAM disponible y usada.
```bash
free -h

#Free --> Sirve para que sea en lenguaje humano.
```	

---

## **Bloque 2: Procesos**

6. Lanza un monitor de procesos en tiempo real y observa:
```bash

ps aux  #Ver todos los procesos que existen en ese momento, con su PID, usuario, uso de CPU/memoria, estado, etc.
# o
top     # Monitorizar en tiempo real el uso de CPU, memoria, carga del sistema y procesos.
#o
htop    # Es como top pero permite desplazamiento horizontal/vertical, búsqueda, filtrado y acciones con teclas de función y tiene una interfaz colorida.

#Para salir  se hace F10 = QUIT --> Fn + F10

```
    
- Número total de procesos.  ->  48
	
- Cuál consume más CPU.   ->  1361
	
- Sal del programa.  ->  q / ctrl + c / F10 = QUIT --> Fn + F10
        
7. Instala y ejecuta una versión mejorada del monitor de procesos y compárala con la anterior.
```bash

sudo apt update
sudo apt install htop

#Muestra mucha más información y da más funcionalidades para navegar por la interfaz.

```
    
8. Obtén un listado de todos los procesos del sistema y localiza el proceso de tu shell.
```bash

ps -lax
# -l listado
# -a ocultos
# -x procesos del usuario actual.

```
    
9. Muestra la jerarquía de procesos en forma de árbol.
```bash
pstree
```
    
10. Lanza el comando `ping` contra `google.com` en segundo plano (&) y obtén su identificador de proceso (PID).
```bash
ping google.com&
#Estoy mandadndo el proceso a segundo plano a la vez que lo ejecuto.

Ctrl + Z --> Suspende el proceso actual
bg --> Lo enviamos al fondo.
jobs -l --> Comprobamos el PID
kill 4567 --> Matamas el ping ya que tiene ese PID asignado.

```
    
11. Finaliza el proceso de Firefox usando su PID.
```bash
ps aux | grep firefox

```
    
12. Vuelve a lanzarlo y esta vez deténlo, luego reactívalo.
```bash
firefox & -->  Lanzar Firefox en segundo plano
kill -STOP 5678 -->  Detener el proceso (pausar)
kill -CONT 5678 -->  Reanudar el proceso

```
    
13. Crea un script que capture la señal de interrupción (Ctrl+C) y muestre un mensaje en lugar de cerrarse.
```bash

```
    

---

## **Bloque 3: Gestión de servicios con systemd**

14. Consulta el estado del servicio de conexión remota (por ejemplo, `ssh`).
```bash
systemctl status ssh
#Muestra si el servicio ssh está activo y su PID.

```
    
15. Inicia dicho servicio si está instalado.
```bash
#Si esta instalado asi:
sudo systemctl start ssh

#Si no esta instalado asi:
sudo apt update
sudo apt install openssh-server
sudo systemctl start ssh

```
    
16. Desactívalo del arranque automático y vuelve a activarlo.
```bash

sudo systemctl disable ssh #--> Desactivo
sudo systemctl enable ssh #--> Activo

```
    

---

## **Bloque 4: Archivos y directorios**

17. Lista todos los archivos, incluidos los ocultos, en tu directorio personal.
```bash
cd ~
ls -la ~

#Nos vamos al home y luego ejecutamos ls -la ~

```
    
18. Crea una carpeta llamada `prueba`.
```bash
mkdir ~/prueba

#Crea la carpeta directamente dentro de tu directorio personal.

```
    
19. Dentro de esa carpeta, crea un archivo `notas.txt` que contenga el texto “Hola Linux”.
```bash

echo "Hola Linux" > ~/prueba/notas.txt

#Redireccionamos Hola linux un archivo llamado notas.txt dentro de prueba

```
    
20. Copia ese archivo con otro nombre.
```bash
cp ~/prueba/notas.txt ~/prueba/notas_copia.txt
```
    
21. Renombra el archivo copiado.
```bash
mv ~/prueba/notas_copia.txt ~/prueba/notas_renombrado.txt
```
    
22. Borra el archivo renombrado.
```bash
rm ~/prueba/notas_renombrado.txt

```
    

---

## **Bloque 5: Redirecciones y pipes**

23. Redirige la salida de un listado de archivos a un archivo llamado `listado.txt`.
```bash
ls > listado.txt

#La salida de ls se redirije al archivo y se reescribe si ya existe.

```
    
24. Añade una nueva línea al final del mismo archivo con el texto "Fin del listado".
```bash
echo "Fin del listado" >> listado.txt
#Agrega el texto al final sin sobreescribir.

```
    
25. Redirige los errores (2) de una operación no válida (`let a=3/0`) a un dispositivo nulo para ignorarlos.
```bash

```
    
26. Filtra de una lista de procesos únicamente aquellos que contengan la palabra “bash”.
```bash
ps aux | grep bash

#Filtran por lo procesos que contengan "bash"

```
    
27. Muestra solo las últimas 5 líneas del archivo `listado.txt`.
    
```bash
tail -n 5 listado.txt

#Muestra las ultimas lineas dle archivo en este caso las ultimas 5.

```
    

---

## **Bloque 6: Tuberías con nombre y sockets**

28. Crea una tubería con nombre llamada `cola`.
```bash
mkfifo cola
```
    
29. Desde una terminal, deja el archivo `cola` en espera de datos. Desde otra terminal, escribe un mensaje en esa tubería.
```bash
tty1 -->
cat cola

tty2 -->
echo hola caracola > cola

```
    
30. Verifica que `cola` es realmente una tubería.
```bash

ls -l cola

```
    
31. Establece un canal de comunicación entre dos terminales locales utilizando una herramienta que permite redirigir flujos de entrada y salida entre sockets.
```bash
#tt1 --->
sudo apt install socat
socat -u TCP-LISTEN:7777 STDOUT

#tty2 --->
socat -u STDIN TCP:127.0.0.1:7777
```
    

---

## **Bloque 7: Redes**

32. Comprueba la conectividad con el servidor `google.com` enviando unos pocos paquetes.
```bash
ping -c 4 google.com

#Hace ping con solamente 4 paquetes.

```
    
33. Muestra la configuración de tus interfaces de red.
```bash
ip a


```
    
34. Revisa qué puertos están en escucha en tu máquina.
```bash
ss -tuln

#Muestra la lista puertos TCP/UDP abiertos.

```
    
35. Consulta la dirección IP asociada al dominio `google.com`.
```bash
host google.com


```
    
36. Realiza la misma consulta de resolución DNS usando otra herramienta distinta.
```bash

dig google.com


```
    
37. Conéctate de forma remota a otra máquina mediante un protocolo seguro (si tienes acceso).
```bash

ssh xandru14@ip_DE_MI_MAQUINA


```
    
38. Copia un archivo desde tu máquina a otra mediante una conexión remota segura.
```bash
scp -P 2222 xandru14@127.0.0.1:~/.bash_history ./historial_ubuntu.txt

```
    

---

## **Bloque 8: Usuarios y permisos**
### Lo hacemos con permisos de superusuario ( sudo )

39. Crea un usuario de prueba llamado `alumno1`.
```bash
sudo adduser alumno1
```
    
40. Cámbiale la contraseña.
```bash

sudo passwd alumno1 -->

Enter new UNIX password: 12345
Retype new UNIX password: 12345
passwd: password updated successfully



```
    
41. Cambia los permisos de un archivo a `755`.
```bash

chmod 755 archivo.txt

```
    
42. Cambia el propietario de un archivo a otro usuario.
```bash
sudo chown usuario2 archivo.txt

```
    
43. Elimina el usuario creado.
```bash

sudo deluser alumno1

```
    

---

