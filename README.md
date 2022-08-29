# curso-webpack

## Apuntes del curso 

- Que es WEBPACK?
    * Es una herramienta que nos va a permitir preparar nuestro código para enviarlo a producción 
    * Nos permite trabajar no solo con JavaScript sino con archivos estaticos, CSS, imagenes, fuentes
    * Tener un modo en desarrollo que nos permita trabajar con cada una de as particularidades de nuestro proyecto
    * Nacio en el 2012
    * Gestionar las dependencias 
    * Ejecutar tareas
    * Compresion de formas, archivos CSS, imagenes
    * Habilitar un entorno de desarrollo local que permita hacer las pruebas en nuestra computadora
    * Cargar los modulos de JS, amd, JS o ECMAScript 2015
    - Es muy importante que webpack es una filosofia que nos va a permitir de forma modular 
    - Es una herramienta muy importante en el desarrollo web del lado del front-end

- Conceptos Basicos de Webpack
    + Webpack es un paquete de modulos estáticos para aplicaciones de JS modernas, webpack lo que hace es que construye un gráfico de dependencias que mapea cada módulo para convertirlo en uno o más módulos segun sea el caso.
        - Desde webpack 4 ya no dependemos de tener un archivo de configuración podemos trabajar con un estándar que se crea, pero para esto debemos entender que debemos tener un punto de entrada dentro de una carpeta especifica y un archivo llamado 
            - index.js
        - vamos a considerar que debemos trabajar con un punto de salida donde va ser creado nuestro poryecto una vez preparado por medio de webpack
            - carpeta DIST que viene de distrinution, aquí se van a añadir los elementos que nosotros estamos preparando con webpack, imagenes, JavaSCript, HTML...
        - vamos a contar con elementos particulares con los que vamos a poder trabajar 
            - modo de producción 
            - modo de desarrollo
            - opción para observar los cambios en tiempo real y recompilar nuestro código, para analizar cada cambio en nuestro proyecto
        - otra cosa que le da mucho valor a webpack es que dispone de LOADERS y PLUGGINS que nos ayudan a preparar particularidades de nuestro proyecto
            - podemos preparar un LOADER para entender un lenguaje particular 
                - React, en el que vamos a utilizar JSX, la sintaxis que nos permite trabajar XML, HTML dentro de React y con esto poder utilizar este mismo loader para identificar esta sintaxis para entender y trabajar nuestro proyecto
                - Los PLUGGINS van a extender estos recursos que ya pedemos agregar con los loaders pero para añadir algunas configuraciones o algunos elementos particulares que nos van a permitir trabajar con cada uno de estos recursos
                - Vamos a poder tener modos de PERFORMANCE donde vamos a poder añadir configuraciones más avanzadas que nos va a permitir a nosotros configurar cómo se va a minificar nuestro proyecto, hacia donde lo vamos a enviar o que carpeta va a ser el destino de nuestros elementos
                - Tener un entorno de desarrollo local que nos permita tener un puerto especifico y poder ver los cambios en RealTime

# CONFIGURACIÓN
- Crear la carpeta desde la terminal mkdir nombre_carpeta
- Ininicializar, es muy importante porque nos va a ayudar a tener nuestro proyecto totalmente listo para trabajar con todo lo que va a ser git, subirlo a la nube, así como tambien com NPM, poder instalar las dependencias que el algún momento vamos a necesitar en este proyecti
    + git init
- Ahora tenemos dos opciones
    + npm init -y --> Hace una configuración por defecto
    + npm init --> para configurar cada uno de los pasos 
- Para abrir mi editor de código (Visual Studio)
    + code .
- Generalmente solemos tener una estructura 
    + Crear carpeta src
        - index.js --> Este archivo va a tener la lógica, es mi punto de entrada, mi punto principal donde voy a tener mi código
    + Trabajar la estructura de elementos que vamos a tener
        - Componentes
        - Paginas
        - Utilerias (utils)
        - archivos
- Instalación de webpack
    + npm install webpack webpack-cli -D
        - webpack-cli: para poder trabajar con comandos dentro de nuestra terminal
        - -D: para guardarlo como una dependencia de desarrollo
- No hemos instalado webpack de manera global, solamente dentro de nuestro proyecto
    + npx webpack
        - npx: para que pueda ejecutarlo dentro de lo que viene siendo un comando
        * Al darle enter va a ubicar el archivo index y nos va a preparar el proyecto
        - webpack optimiza nuestro código para ser mejor, elimina las redundacias, etc...
    + npx webpack --mode development
        - --mode development: para ejecutar el modo desarrollo
    + npx webpack --mode production

## CONSTRUCCIÓN DEL PROYECTO
- crear un archivo en la raiz de nuestro proyecto
    + webpack.config.js -> aquí va a vivir toda la configuración que vamos a realizar para nuestro proyecto
        * Vamos a preparar este archivo para que entienda cual es nuestro punto de entrada, cuales van a ser las extensiones que vamos a estar usando
    + vamos a crear una constante que le vamos a llamar path, va a utilizar un REQUIRE que me va a ayudar a traer el elemento path, path ya esta disponible en node así que no hay que hacer una instalación de dependencias
        - const path = require('path');
    + Vamos a crear un modulo que vamos a exportar con un objeto con la configuracion deseada  
        - entry: el punto de entrada de nuestra aplicación
        - output: es hacia donde vamos a enviar lo que va a preparar webpack, webpack ya tiene una carpeta para esto que es la carpeta dist. Aqui dentro en un objeto interno vamos a añadir los elementos con los que vamos a trabajar
            - path, vamos a traer el path que trajimos al inicio de nuestro proyecto para tener el uso de resolve que nos va a permitir saber donde se encuentra nuestro proyecto, en que directorio y poderlo usar de esta forma no tener un problema particularmente con el nombre de la carpeta donde estoy posicionado. etc... Asi cuando enviamos nuestro proyecto a un servidor en la nube tener la direcccion de donde se va porder encontrar este repositorio, archivo ... con eso garantizamos que siempre va a poder encontrar la carpeta donde se encuentra este proyecto
            - filename, podemos ponerle un nombre, bundle mas adelante podemos ponerle un hash
        - Queremos pasarle a esta configuracion de webpack las extensiones con las que vamos a trabajar de la siguiente manera 
            - resolve: creamos un objeto y dentro de ese objeto le pasamos lo siguiente
                - extesions: dentro de un arreglo le pasamos las extensiones que vamos a utilizar
        # module.exports = {
            entry: index.js,
            output: {
                path: path.resolve(__dirname, 'dist'),
                filename: 'main.js',
            },
            resolve: {
                extensions: ['.js']
            }
    ##   }  // aqui vamos a añadir todas las configuraciones

    - despues de crear todas estas configuraciones vamos a ir a la terminal y correr el siguiente comando
        + npx webpack --mode production --config webpack.config.js
    - para hacer mas amigable la ejecucion del comando podemos ir a package.json y crear un script 
        + "build": "webpack --mode production"

## BABEL
Con este preparamos nuestro código JavaScript para que sea compatible con todos los navegadores
- Debemos integrar babel a nuestro proyecto y a la configuración de webpack para sacarle todo el provecho posible 
    * Añadimos unas dependencias que vamos a trabajar, instalamos en nuestra terminal éstas mismas  
        - npm install babel-loader @babel/core @babel/preset-env @babel/plugin-transform-runtime -D
            + @babel/preset-env: nos va a ayudar a trabajar con JavaScript moderno
            + @babel/plugin-transform-runtime: Nos va a servir para trabajar con asincronismo
    * Añadimos una configuración especifica, creamos en src un archivo de nombre .babelrc
    - El punto en sistemas operativos UNIX es un archivo oculto, simplemente no es visible a simple vista por el usuario y en este caso es usado para añadir configuraciones
        # dentro del archivo .babelrc
            {
                "presets": [
                    "@babel/preset-env"
                ],
                "plugins": [
                    "@babel/plugin-transform-runtime"
                ]
            }
    - Despues de añadir esto al archivo de babel, ahora lo vamos a añadir a nuestro archivo de webpack
        # module.exports = {
            entry: index.js,
            output: {
                path: path.resolve(__dirname, 'dist'),
                filename: 'main.js',
            },
            resolve: {
                extensions: ['.js']
            },
            module: {
                rules: [
                    {
                        test: /\.m?js/,
                        exclude: /node_modules/,
                        use: {
                            loader: 'babel-loader'
                        }
                    }
                ]
            }
    ##   }  // aqui vamos a añadir todas las configuraciones
        - test: para saber que tipo de extensiones utilizaremos, es necesario trabajar con expresiones regulares 
            -- /\.m?.js$/
                cualquier archivo que empiece por m (de module .mjs) o .js
        - exclude: para decirle que no incluya o que excluya ciertas cosas
            -- /node_modules
        - use: para pasarle internamente el loader que vamos a utilizar 
            -- loader: 'babel-loader'

## HTML en Webpack
- npm install html-webpack-plugin -D
    * Luego vamos a nuestro archivo webpack.config para añadir este elemento
        -- creamos una constante 
            const HtmlWebpackPlugin = require('html-webpack-plugin');
    const path = require('path');
    const HtmlWebpackPlugin = require('html-webpack-plugin');

    module.exports = {
        entry: './src/index.js',
        output: {
            path: path.resolve(__dirname, 'dist'),
            filename: 'main.js',
        },
        resolve: {
            extensions: ['.js']
        },
        module: {
            rules: [
                {
                    test: /\.m?js/,
                    exclude: /node_modules/,
                    use: {
                        loader: 'babel-loader'
                    }
                }
            ]
        },
        plugins: [
            new HtmlWebpackPlugin({
                inject: true,
                template: './public/index.html',
                filename: './index.html'
            })
        ]
    }
// Ahora en package.json agregamos un nuevo script
    "dev": "webpack --mode development"

## Loaders para CSS y preprocesadores de CSS
1. Instalamos las dependencias que vamos a utilizar
    - CSS loader
    - plugin para trabajar con CSS en diferentes partes de nuestra aplicación y unirlos
        * npm install mini-css-extract-plugin css-loader -D

2. Ahora vamos a indentificar en la carpeta src nuestro archivo index.js, vamos a importar los estilos 
    * import './styles/main.css'

3. Ahora vamos a añadir la configuración a webpack
    const path = require('path');
    const HtmlWebpackPlugin = require('html-webpack-plugin');
    ++const MiniCssExtractPlugin = require('mini-css-extract-plugin');

    module.exports = {
        entry: './src/index.js',
        output: {
            path: path.resolve(__dirname, 'dist'),
            filename: 'main.js',
        },
        resolve: {
            extensions: ['.js']
        },
        module: {
            rules: [
                {
                    test: /\.m?js/,
                    exclude: /node_modules/,
                    use: {
                        loader: 'babel-loader'
                    }
                },
                {
                    ++test: /\.css$/i,
                    ++use: [MiniCssExtractPlugin.loader,
                    'css-loader'
                    ],
                }
            ]
        },
        plugins: [
            new HtmlWebpackPlugin({
                inject: true,
                template: './public/index.html',
                filename: './index.html'
            }),
            ++new MiniCssExtractPlugin(),
        ]
    }
    NOTA: no va con los simbolos '++', es simplemente para denotar que se añadieron elementos nuevos para esta configuración en particular

## Loader para los preprocesadores en este caso STYLUS
* npm install stylus stylus-loader -D
    const path = require('path');
    const HtmlWebpackPlugin = require('html-webpack-plugin');
    const MiniCssExtractPlugin = require('mini-css-extract-plugin');

    module.exports = {
        entry: './src/index.js',
        output: {
            path: path.resolve(__dirname, 'dist'),
            filename: 'main.js',
        },
        resolve: {
            extensions: ['.js']
        },
        module: {
            rules: [
                {
                    test: /\.m?js/,
                    exclude: /node_modules/,
                    use: {
                        loader: 'babel-loader'
                    }
                },
                {
                    ++test: /\.css|.styl$/i,
                    use: [MiniCssExtractPlugin.loader,
                    'css-loader',
                    'stylus-loader'
                    ],
                }
            ]
        },
        plugins: [
            new HtmlWebpackPlugin({
                inject: true,
                template: './public/index.html',
                filename: './index.html'
            }),
           +++new MiniCssExtractPlugin(),
        ]
    }
-- ahora creamos un archivo en la carpeta styles 
    * vars.styl

## Copia de archivos con webpack
    - Podemos utilizar un plugin que se llama copy-webpack
        * npm install copy-webpack-plugin -D
    - Configuramos que elementos necesitamos mover
    - Vamos a copiar nuestro archivo de imagenes hacia la carpeta distribution y vamos a ligar correctamente este template para que pueda funcionar de manera correcta
    ----------------------------------------------------
    const CopyPlugin = require('copy-webpack-plugin');
    module.exports = {
        ...
        plugins: [
            new HtmlWebpackPlugin({
                inject: true,
                template: './public/index.html',
                filename: './index.html'
            }),
            new MiniCssExtractPlugin(),
            new CopyPlugin({
                patterns: [
                    {
                        from: path.resolve(__dirname, "src", "assets/images"),
                        to: "assets/images"
                    }
                ]
            })
        ]
    }
    -- from: path.resolve(__dirname, 'src', 'assets/images')
    Con esto decimos que aqui se encuentran los archivos que vamos a mover, podemos mover solo un archivo o toda la carpeta

## Loaders de imagenes
    rules: [
        ...
        {
            test: /\.png/,
            type: 'asset/resource'
        }
    ]
En templates importamos las imagenes y las agregamos a la etiqueta img en src como una variabla de javascript

## Loaders de Fuentes