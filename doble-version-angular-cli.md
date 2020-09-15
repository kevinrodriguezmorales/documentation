# Instalar distintas versiones de Angular CLI
---

Debido a un requirimiento de trabajar en un proyecto con una versión en especifico de Angular, es que se decidio mantener la versión recientemente instalada(10) y ademas trabajar con Angular 7. A continuación se detallan los pasos para mantener ambas versiones:

- **1° - Instalar CLI 10 globalmente :**

```cmd
    npm install -g @angular/cli
```
- **2° - Crear una carpeta para los proyectos Angular 7 :**

```cmd
    mkdir ng7
    cd ng7
```
- **3° - Crear una aplicación `npm` local :** dentro de `ng7`
```cmd
    npm init -y
```
- **4° - Instalar CLI 7 localmente ***(v7-lts: 7.3.10)*** :** para conocer otras versiones ejecutamos `npm view @angular/cli`
```cmd
    npm install @angular/cli@7.3.10
``` 
En este paso, dentro de la carpeta `ng7` podrás ver 3 archivos: una carpeta `node_modules`, `package.json` y `package-lock.json`. Dentro de `package.json` podras ver la versión de Angular CLI instalada.
- **5° - Eliminamos :** los archivos `package.json` y `package-lock.json` para que al correr `ng new` no se generen conflictos(quizás sea necesario cerrar y volver a abrir cmd), si no se eleminan estos archivos `ng` asume que esta creando una nueva app dentro de una ya existente.
- **6° - Creamos la nueva app :**
```cmd
    ng new proyect-angular7
```

Desde este momento, todos los proyectos que se creen dentro de la carpeta `ng7` van a pertenecer a la versión **7.3.10**, crearla fuera de esta seran tomadas como versiones **10.1.0**(versión al momento de escribir esta guía).

Una vez que las dependencias sean instaladas y querramos correr el proyecto localmente(navegador), posiblemente el comando `npm start` o `ng serve` no funcionen como se espera, entonces se pueden seguir una de las siguientes opciones:

- 1° - Usando la ruta del siguiente archivo
```cmd
    node_modules/.bin/ng serve
```
- 2° - Configurar el script de `npm`: en el `package.json` se puede crear un script que corra los comandos que se necesiten. Cuando se tiene el script de `npm`, siempre se va a ejecutar los comandos con las versiones instaladas localmente. El script se puede parecer a algo como esto:
```cmd
    "scripts": {
        "start": "ng serve",
```
Si aún así hubieran problemas, podemos asegurarnos que se ejecute el comando en la versión local colocando la ruta:
```cmd
    "scripts": {
        "start": "./node-modules/.bin/ng serve",
```

Para las pruebas de esta guía se uso la primera opción, despues de eso paramos el `localhost`: `ctrl` + `C` y se volvio a ejecutar el comando `ng serve` o `npm start`, funcionando en ambos casos.

<!-- serverless config credentials --provider aws --key AKIAXRRJRY4L6HWIPVVR --secret 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 -->