# Camera DMK41AU02.AS Repository 
Código GNU/Linux y firmware UVC para la cámara 41AU02.AS

## Guía rápida de instalación del firmware de la cámara y ejecución de un programa de ejemplo en lenguaje C. 

Las instrucciones de este manual instala el software en el sistema de ficheros, concretamente en la localización: /usr
Si se quiere instalar el software en un directorio diferente (ej: /home/<your_name_user>), necesita cambiar la ruta en la instalación.

## Versión de Ubuntu donde se ha probado
```
$ lsb_release -a
Distributor ID:	Ubuntu
Description:	Ubuntu 16.04.3 LTS
Release:	16.04
Codename:	xenial
```
## Instalar Dependencias

```
# Build dependencias
sudo apt-get install git g++ cmake pkg-config libudev-dev libudev1 libtinyxml-dev libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev libglib2.0-dev libgirepository1.0-dev libusb-1.0-0-dev libzip-dev uvcdynctrl python-setuptools libxml2-dev libpcap-dev libaudit-dev libnotify-dev autoconf intltool gtk-doc-tools

# Runtime dependencias
sudo apt-get install gstreamer1.0-tools gstreamer1.0-x gstreamer1.0-plugins-base gstreamer1.0-plugins-good gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly libxml2 libpcap0.8 libaudit1 libnotify4

sudo apt-get install libgtk-3-dev libnotify-dev
```

### Building

Los siguientes comandos construirán e instalarán nuestro software con la configuración predeterminada. 

```
git clone --recursive https://github.com/AlvaroConvilla/camera_DMK41AU02.AS.git
cd camera_DMK41AU02.AS
mkdir build
cd build

cmake -DBUILD_ARAVIS=ON -DBUILD_GST_1_0=ON -DBUILD_TOOLS=ON -DBUILD_V4L2=ON -DCMAKE_INSTALL_PREFIX=/usr ..


make
sudo make install
```
### Para que el sistema operativo detecte la cámara:
```
cd camera_DMK41AU02.AS
sudo cp data/udev/80-theimagingsource-cameras.rules /etc/udev/rules.d/
sudo service udev restart
```

### Ejemplo de visualización de la cámara en lenguaje C.
```
cd examples/c
make
./properties
```
Las imagenes que se capturen se guardan en ficheros(.jpg) en el path: /tmp
Para ello:
```
sudo su
cd /tmp
ls -l
display image-xxxxxx.jpg
```

### Para mayor información

Visita el Repositorio oficial con información más detallada: https://github.com/TheImagingSource/tiscamera