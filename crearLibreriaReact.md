# 📘 Crea tu propia librería de Componentes

### Paso a paso para crear librería

1. Crear una carpena donde se va a almacenar la librería
2. Correr el siguiente comando ```npm install --save-dev react react-dom typescript @types/react``` para instalar las dependencias de react
3. Correr el siguiente comando ```npx tsc --init``` para crear el archivo tsconfig.json
4. Agregar esta configuración en el archivo de tsconfig.json

```{
"compilerOptions": {
    "jsx": "react",
    "target": "es2016",
    "outDir": "dist",
    "allowJs": true,
    "skipLibCheck": true,
    "strict": true,
    "forceConsistentCasingInFileNames": true,
    "module": "ES2020",
    "allowSyntheticDefaultImports": true,
    "moduleResolution": "Node",
    "declaration": true,
    "declarationDir": "dist"
},
"include": [
    "stories"
    ]
}
```

5. Correr el siguiente comando ```npx sb init``` para instalar Storybook

6. Correr el siguiente comando ```npm run storybook``` iniciar Storybook

### Hasta este paso puede ser un proyecto normal, lo siguiente es necesario SOLO para crear una librería

7.  Correr el siguiente comando ```npm i --save-dev rollup @rollup/plugin-node-resolve @rollup/plugin-babel rollup-plugin-uglify rollup-plugin-postcss rollup-plugin-typescript2 rollup-plugin-peer-deps-external``` 
para instalar las dependencias necesarias para genera la librería 

8. Crear el archivo ```rollup.config.js``` en la raíz del proyecto

9. En el archivo ```rollup.config.js``` agregar la siguiente configuración
```
import peerDepsExternal from 'rollup-plugin-peer-deps-external'
import resolve from "@rollup/plugin-node-resolve";
import typescript from "rollup-plugin-typescript2";
import postcss from "rollup-plugin-postcss";
import { uglify } from "rollup-plugin-uglify";
import { babel } from '@rollup/plugin-babel';

export default {
    input: "./index.ts",
    output: [
        {
            file: "dist/index.js",
            format: 'es'
        }
    ],
    plugins: [
        peerDepsExternal(),
        resolve(),
        typescript(),
        postcss({
            extensions: ['.css']
        }),
        uglify(),
        babel()
    ]
}
```

10. Agregar el siguiente script en el archivo package.json```"buildLib": "rollup -c"```

11. Crear una cuenta en npm account - https://www.npmjs.com/

12. Correr el comando ```npm login``` y autenticarse

13. Agregar nombre y versión del la dependencia 
```
"name": "@[tu-usuario]/react-library",
"version": "1.0.0",
```
14. Correr el comando ```npm publish --access=public``` para publicar la librería en NPM



