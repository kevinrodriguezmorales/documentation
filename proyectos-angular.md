# Proyectos Angular

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 9.1.1.

## Development server

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The app will automatically reload if you change any of the source files.

## Code scaffolding

Run `ng generate component component-name` to generate a new component. You can also use `ng generate directive|pipe|service|class|guard|interface|enum|module`.

## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory. Use the `--prod` flag for a production build.

## Running unit tests

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Running end-to-end tests

Run `ng e2e` to execute the end-to-end tests via [Protractor](http://www.protractortest.org/).

## Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI README](https://github.com/angular/angular-cli/blob/master/README.md).

## Inicializando el proyecto

En la creación y despliegue del proyecto se generaron algunos contra tiempos debido a conflictos generados al correr comandos de `npm` y `ng` tales como

```cmd
    $ ng new app-name
    $ npm install
    & npm start

    # npm WARN deprecated core-js@2.6.11: core-js@<3 is no longer maintained and not recommended for usage due to the number of issues
```

Esto se resolvió abriendo el Windows Powershell **como administrador**

```cmd
    $ npm cache clean --force
    # npm WARN using --force I sure hope you know what you are doing.

    $ npm install -g @angular/cli
    # @angular/cli@9.1.1
      updated 1 package in 236.724s
```

Seguidamente se pasa a crear el proyecto nuevamente

```cmd
    $ ng new <name-project> --style=scss --inline-style
    $ npm install
    $ npm start
    #: Compiled successfully.
```

explicación del comando

- **ng** es el comando instalado por @angular/cli previamente.
- **new OR n** es un argumento que recibe ng el cual le decimos que es un proyecto nuevo.
- **name-project** es el nombre que le daremos a la carpeta de nuestro proyecto.
- **--style=scss** con este argumento le decimos a nuestros proyecto que ocuparemos el pre procesador sass.
- **--inline-style** de la documentación: incluye estilos en línea en el archivo TS del componente. De forma predeterminada, se crea un archivo de estilos externo y se hace referencia a él en el archivo TS del componente.

Opcionales

- **--prefix=ngWork** el prefijo que llevará todos los componentes de la aplicación.
- **--skip-git** es para evitar la creación de la carpeta git.

## Estructura del Proyecto

Como base inicial para cualquier proyecto se recomienda la siguiente estructura de carpetas

~~~
store-app/src/app
.
├── app.component.html
├── app.component.specs.ts
├── app.component.ts
├── app.module.ts
├── app-routing.module.ts
├── /@pages
├── /@core
|    ├── /directives
|    └── /material-design
├── /@shared
|    └── /components
|       ├── /banner-main
|       ├── /card-product
|       ├── /footer
|       ├── /navbar
|       |    ├── navbar.component.html
|       |    ├── navbar.component.ts
|       |    ├── navbar.component.specs.ts
|       |    └── navbar.component.scss
|       └── /sidenav
|       |    ├── sidenav.component.html
|       |    ├── sidenav.component.ts
|       |    ├── sidenav.component.specs.ts
|       |    └── sidenav.component.scss
|       └── components.module.ts
~~~

## Configuración de Estilos, Librerías y Componentes

### Estilos

#### SCSS por defecto

Para nuevos proyectos este comando los creara con archivos sass por defecto

```cmd
    $ ng n project-name --style=scss
```

En el futuro, si se desea utilizar sass de forma predeterminada, puede configurarse en el angular-cli como se muestra a continuación.

```cmd
    $ ng config --global defaults.styleExt = scss
```

#### Styles: de CSS a SCSS

Al crear el proyecto se obvio configurar la creación y lectura de archivos de styles con la extensión `.scss` por lo que se paso a configurar de manera manual, primero ejecutamos el comando:

```cmd
    $ ng config schematics.@schematics/angular:component.styleext scss
    # 
```

luego se paso a cambiar las extensiones de todos los archivos manualmente tanto en modulos y componentes ya creados, así mismo también se cambio las extensiones en cada uno de los arrays `styles` de `angular.json`.
```cmd
    ...
    "styles": [
        ...
        "src/styles.scss"
    ],
    ...
```

### Librerías

En este proyecto se agrego:

* [FontAwesome](https://fontawesome.com/how-to-use/on-the-web/setup/using-package-managers) version 5.12.1.

#### FontAwesome

Para comenzar a usar FontAwesome primero se instala el módulo haciendo uso de `npm` :

``` cmd
    $ npm install --save @fortawesome/fontawesome-free
    # + @fortawesome/fontawesome-free@5.13.0
    # added 1 package from 6 contributors, removed 1 package and audited 16089 packages in 143.457s
```

luego en el archivo `angular.json` agregar lo siguiente

``` javascript
    "styles": [
        "node_modules/@fortawesome/fontawesome-free/css/all.css"
    ]
```

o esto (cualquiera de las dos opciones sirve)

```js
    "scripts": [
        "node_modules/@fortawesome/fontawesome-free/js/all.js"
    ]
```

Finalmente agregamos en el html:

```html
    <i class="fab fa-angular"></i>
```
**Si no renderizara en el navegador, se recomienda parar el servidor local y volver a levantarlo**

Para mayor referencia sobre los iconos y la sintaxis para su uso visitar [font awesome](https://fontawesome.com/icons?d=gallery&m=free). Si se presentará algún problema al momento de renderizar los iconos, podemos parar el servidor local y volver a iniciarlo, si esto no sirviera volvemos a ejecutar `npm install` y luego nuevamente el servidor local.

#### Material Angular

Al instalar Material en nuestro proyecto se establecieron las siguientes opciones

```cmd
    $ ng add @angular/material
    ? Choose a prebuilt theme name, or "custom" for a custom theme
    $ Custom
    ? Set up global Angular Material typography styles?
    $ Yes
    ? Set up browser animations for Angular Material?
    $ Yes
    # √ Packages installed successfully.
```

### Dialog(cuadro de dialogo)

Para usar el Dialog de Material basta con importar ` import {MatDialogModule} from '@angular/material/dialog'; ` y declarar en las importaciones en el módulo principal. También sera necesario crear un componente que será proyectado en el Dialog, por lo que también será necesario declararlo en `entryComponents` dicho componente. Para el caso de Lazy Modules va ser necesario que tambien se importe MatDialogModule, esto si estuvieramos importandolo en un modulo por separado(en MaterialAngularModule por ejemplo).

```typescript
    @NgModule({
        imports: [
            MatDialogModule
        ],
        declarations: [
            AppComponent,
            LoginComponent,
            DashboardComponent,
            HomeComponent,
            DialogResultExampleDialog        
        ],
        entryComponents: [
            DialogResultExampleDialog
        ]
```

#### Bootstrap

Instalamos el paquete de Bootstrap usando `npm`

```cmd
    $ npm i --save bootstrap jquery popper.js
    # + bootstrap@4.4.1
    # + popper.js@1.16.1
    # + jquery@3.5.0
    # added 3 packages from 5 contributors, removed 1 package and audited 16214 packages in 195.802s
```

luego en el archivo de estilos principal de nuestro proyecto `styles.scss` en este caso, importamos los archivos necesarios, para este proyecto solo se hará uso de la cuadricula y sistema de grillas.

```css
    @import '~bootstrap/scss/bootstrap';
    @import '~bootstrap/scss/bootstrap-reboot';
    @import '~bootstrap/scss/bootstrap-grid';

    /* your styles */
```

#### Owl Carousel - ngx-owl-carousel-o

Para agregar interactividad al momento de implementar `sliders`, se agregará **Owl Carousel 2(*)**. Este paquete no necesita soporte de jQuery como el paquete `ngx-owl-carousel`. Comenzemos:

- 1° Instalar
  ```cmd
    $ npm instalar ngx-owl-carousel-o
    # + ngx-owl-carousel-o@4.0.0
    # added 2 packages from 2 contributors and audited 1715 packages in 27.474s
  ```
- 2° Agregar hojas de estilo: para esto podemos elegir entre 2 opciones:
  - Opción 1: agregar en el archivo `angular.json`
    ```json
        "styles": [
              "./node_modules/ngx-owl-carousel-o/lib/styles/prebuilt-themes/owl.carousel.min.css",
              "./node_modules/ngx-owl-carousel-o/lib/styles/prebuilt-themes/owl.theme.default.min.css",
              "src/styles.css"
        ]
    ```
  - Opción 2: agregar en `src/styles.css` o `src/styles.scss`
    ```SCSS
        /* quitar espacios entre @ e import */
        @ import "~ngx-owl-carousel-o/lib/styles/scss/owl.carousel";
        @ import "~ngx-owl-carousel-o/lib/styles/scss/owl.theme.default";
    ```
- 3° Importar(**): importamos en `app.module.ts`:
  ```ts
    import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
    import { CarouselModule } from 'ngx-owl-carousel-o';
    ...

    @NgModule({
        ...
        imports: [
            BrowserAnimationsModule,
            CarouselModule
        ]
        ...
    })
  ```
- 4° Agregar: importamos `OwlOptions` en la clase del componente que se usa para configurar las propiedades del carrusel(se recomienda agregar las opciones del carrusel en `ngOnInit()`):
  ```ts
    ...
    import { OwlOptions } from 'ngx-owl-carousel-o';
    ...

    export class OwlCarouselComponent implements OnInit {

        ...

        public customOptions: OwlOptions;

        constructor() { }

        public ngOnInit() {
            this.customOptions = {
                loop: true,
                mouseDrag: false,
                touchDrag: false,
                pullDrag: false,
                dots: false,
                navSpeed: 700,
                navText: ['Previous', 'Next'],
                responsive: {
                0: {
                    items: 1 
                },
                400: {
                    items: 2
                },
                740: {
                    items: 3
                },
                940: {
                    items: 4
                }
                },
                nav: true
            }
        }

        ...
    }
  ```
  Luego en el `html` agregamos un `owl-carousel-o` componente de directiva para envolver `carouselSlide`, directivas múltiples para cada diapositiva como se muestra a continuación:
  ```html
    <owl-carousel-o [options]="customOptions">
        <ng-template carouselSlide>
            <div class="slide">
                <img src="https://i.picsum.photos/id/905/400/300.jpg">
            </div>
        </ng-template>
        <ng-template carouselSlide>
            <div class="slide">
                <img src="https://i.picsum.photos/id/507/400/300.jpg">
            </div>
        </ng-template>
        <ng-template carouselSlide>
            <div class="slide">
                <img src="https://i.picsum.photos/id/609/400/300.jpg">
            </div>
        </ng-template>
    </owl-carousel-o>
  ```

**( * )** Al encontrar documentación sobre esta paquete, referian que se podia usar en Angular verisones 7, 8 y 9(7 para el proyecto en el que se implementó), pero una vez instalado y al comenzar a usar la etiqueta `<owl-carousel-o></owl-carousel-o>` mostraba un error de compatibilidad:
```cmd
# ERROR in node_modules/ngx-owl-carousel-o/lib/carousel/carousel.component.d.ts(29,9): error TS1086: An accessor cannot be declared in an ambient context.
# node_modules/ngx-owl-carousel-o/lib/carousel/carousel.component.d.ts(30,9): error TS1086: An accessor cannot be declared in an ambient context.
```
Entre algunas soluciones encontradas, recomendaban actualizar a Angular 8, pero esto no era posible porque era menester mantener la version 7, la solución encontrada fue agregar una propiedad en `tsconfing.json`:
```json
    {
        ...
        "compilerOptions": {
            "skipLibCheck": true,
            ...
        }
    }
```

**( ** )** al importar `CarouselModule` se sugiere importar desde el modulo que se va a utilizar, durante el desarrollo de este documento se trabajo en un proyecto que importa `ComponentsModule` en `app.module.ts` y es en este en el que se importa `CarouselModule`, si el alcance que se estima de la librería es global, entonces tiene mas sentido importar en `app.module.ts`. En cuanto a `BrowserAnimationsModule` se recomienda importar en el modulo principal(`app.module.ts`) ya que puede generar un error:
```cmd
ERROR Error: Uncaught (in promise): Error: BrowserModule has already been loaded. If you need access to common directives such as NgIf and NgFor from a lazy loaded module, import CommonModule instead.
```

Los pasos de instalación fueron tomados de [Adding Owl Carousel in Angular 7/8/9](https://medium.com/@shreyakaushik11/adding-owl-carousel-in-angular-7-8-9-67f401665ee2) y de otras fuentes en internet así como las soluciones a los problemas que se fueron presentando, para conocer más información sobre este paquete: eventos, métodos, compatibilidad, etc. visitar [ngx-búho-carrusel-o](https://www.npmjs.com/package/ngx-owl-carousel-o).

### Contentful [Contentful](https://www.contentful.com/developers/docs/javascript/tutorials/using-contentful-in-an-angular-project/)

```cmd
    $ npm i --save contentful
```

```ts
    import { createClient, Entry } from 'contentful';
```

### Componentes

Para el desarrollo del siguiente proyecto, desde el diseño, la línea gráfica fue basada en la documentación de [Material Design](https://material.io/), por lo que muchos componentes se basan en la anatomía de los construidos en [Angular Material](). Las siguientes secciones describen de manera breve la importación, configuración y despliegue de algunos componentes Angular.

#### Barra Lateral de Navegación - [Angular Material sidenav](https://material.angular.io/components/sidenav/api)

Empezamos por importar el component 

#### [mydatepicker](https://www.npmjs.com/package/mydatepicker)
