# Ejercicios del tema 2: Desarrollo basado en pruebas
### Ejercicio 1
**Instalar alguno de los entornos virtuales de node.js (o de cualquier otro lenguaje con el que se esté familiarizado) y, con ellos, instalar la última versión existente, la versión minor más actual de la 4.x y lo mismo para la 0.11 o alguna impar (de desarrollo).**

Instalamos nvm mediante:
```bash
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.32.0/install.sh | bash
```
Tras reiniciar el terminal, comprobamos que nvm se ha instalado correctametne mediante:
```bash
command -v nvm
```
Instalamos la última versión:
```bash
nvm install node
######################################################################## 100,0%
Computing checksum with sha256sum
Checksums matched!
Now using node v6.8.1 (npm v3.10.8)
Creating default alias: default -> node (-> v6.8.1)
```
De igual forma se instala la versión de desarrollo:
```bash
nvm install v0.11
######################################################################## 100,0%
Computing checksum with sha256sum
Checksums matched!
Now using node v0.11.16 (npm v2.3.0)
```
Para hacer el cambio entre versiones se usa el comando _nvm use version-a-usar_ como por ejemplo:
```bash
nvm use v6.8.1
```
