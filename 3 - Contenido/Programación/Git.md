Para solucionar cosas del estilo de generar una versión y querer hacerle cambios, como sacarle algo, modificar, etc. y después cada archivo tiene muchas ramas. Además se tiene un historial de cambios desconocidos.

Git no es lo mismo que GitHub
Git: Sistema de control de versiones

Se tiene el working directory: Es el espacio de trabajo actual. Con los archivos, códigos, etc. Es en el propio computador (como un escritorio con papeles).
Staging Area: Se agrupan y preparan los cambios específicos, se trata de agrupar los cambios afines en las mismas cajas.

Local Repository, Commit: Sellar la caja. Git toma una fotografía (es permanente) de los archivos que estaban en la caja. Se asocia un registro histórico de los cambios.

Remote Repository(GitHub): Se envían al repositorio remoto las 'cajas'. Se sincroniza el trabajo propio con el del servidor.



trabajo a caja:
git add 'archivo'

sellar caja: git commit

mandar codigo: git push


Rama/Branch
Para probar algo nuevo pero sin querer cambiar el código.
-O-O-O-O-O-
cada círculo es un cambio que se hizo.
Se puede sacar una línea de tiempo alternativa para hacer cambios:

Cambiando entre ramas se va a tener distinto código, para ver todas las ramas de un repositorio: git branch
- Para crear una rama sin cambiarse a ella: git branch 'name'
- Para cambiarse a esa rama: git switch; también está checkout pero tiene otra funcionalidad como borrar el código anteriormente modificado.
Para combinar 

En general, en entornos formales se hace un pull request para autorizar la mezcla (merge) del código a la rama.


CONFIG
después de instalar:
git config --global user.name 'nombre cualquiera, da igual'
gti config --global user.email 'EMAIL DE GITHUB'
se debe usar el mismo mail q en github para ver el historial.

Clonar repositorio
Tomar el repositorio del servidor y traerlo.
1. Con HTTPS: Es la maś fácil, se usa un enlace web normal y GitHub guarda una Personal Access Token q se ingresa en cada commit
2. SSH: Se crea una llave criptográfica en el pc para que github 'confíe' en ella y no se necesita meter clave en cada 

git clone git@



GITHUB
Plataforma en línea para alojar, compartir el código.
