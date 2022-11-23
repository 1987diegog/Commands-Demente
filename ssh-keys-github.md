# Llaves SSH - Github!

Al crear nuestras llaves SSH podemos otorgarle la misma a GitHub, GitLab, etc para comunicarnos de forma segura y sin necesidad de escribir nuestro usuario y contraseña todo el tiempo.

## Generar Key SSH con keygen
```
ssh-keygen -t rsa -b 4096 -C "1987diegog@gmail.com"
```
*Banderas utilizadas*
**-t** *rsa* --- especifica el algoritmo que vamos a utilizar para generar la llave
**-b** *4096* --- indicamos que tan compleja será la llave
**-C** *"1987diegog@gmail.com"* --- a que correo electrónico va a estar conectada esta llave

Si todo va bien deberá pedirnos donde vamos a guardar nuestra llave ssh, el que indica por defecto es un muy buen lugar para hacerlo, por lo tanto, solo le damos **>Enter**.
> Generating public/private rsa key pair. 
> Enter file in which to save the key (/home/username/.ssh/**id_rsa**):

En este ejemplo "id_rsa" será el nombre que se tomará para generar la clave publica y privada generando dos archivos como los siguientes:

- id_rsa
- id_rsa.pub

> Si quisieramos cambiar el nombre de la key ssh, bastaría con indicar otro como por ejemplo: 
/home/username/.ssh/**dementeSSHIdeas**

- dementeSSHIdeas
- dementeSSHIdeas.pub

Para mayor seguridad nos solicitará una *contraseña extra* "*passphrase*", que es lo recomendado, pero también puede dejarse vacía en caso de NO querer ingresarla cada vez que se solicite nuestra llave ssh, la ingresamos y continuamos con **>Enter**.
>Enter passphrase (empty for no passphrase): 

Si todo ha ido bien habremos generado la llave, nos mostrará un mensaje donde podremos ver el *fingerprint* 
```
SHA256:dpTcz6UfK7nouyZ2KyFI8BsJzjQ+jKyAQbW-UDMQvTq 1987diegog@gmail.com
```


como también el *randomart image*.
```
+---[RSA 4096]----+
| ..o.            |
| ..o.-     + .  .|
|. .=J =   . = .o.|
|. +Y.* + . ..o o=|
|.o..+ o S    . .+|
|o .U.o M . .  o  |
|. ==      o ..   |
| o         =...  |
|          .o=+.  |
+----[SHA256]-----+
```

## Comprobar servidor de llaves SSH 
Verificar que el "servidor de llaves ssh" este corriendo, para esto utilizamos *eval*
```java
eval $(ssh-agent -s)
```
si el servidor de llaves ssh se encuentra levantado deberá mostrar algo similar a lo siguiente:
```java
Agent pid 51177
```
## Añadir la llave SSH al servidor
Se debe agregar la llave ssh **privada**, la misma no tiene extensión, ejemplo:
```java
ssh-add ~/.ssh/id_rsa  
```
Al agregarse nos deberá mostrar un mensaje similar al siguiente:
```
Identity added: /home/username/.ssh/id_rsa (1987diegog@gmail.com)
```

## Añadir la llave SSH a GitHub
Se debe agregar la llave ssh **publica**, con extensión **".pub"**, ejemplo:
```
~/.ssh/id_rsa.pub
```
Clonar repositorio con SSH
```
git clone git@github.com:1987diegog/proyect.git
```
En caso de ya tener el repositorio clonado se puede cambiar el acceso al mismo utilizando la clave SSH de la siguiente forma:
```
git remote set-url origin git@github.com:1987diegog/proyect.git
```

Posiblemente como paso final se deba autorizar la llave en GitHub, para esto:

```Configure SSO -> authorize```

