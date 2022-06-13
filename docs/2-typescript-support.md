# TypeScript support

1. Rename index.js and utils.js to `.ts` files and rename `actions` directory to `actions-src`
2. Install dependencies
   ```
      npm install shx --save-dev
      npm install typescript --save-dev
      npm install "@types/mime-types" --save-dev
      npm install "@types/node-fetch" --save-dev
      npm install "@types/node" --save-dev
      npm install --save-dev eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin
   ```
3. Configure eslint. This tool will allow us to automatically check if our code follows recommended standards. Create `.eslintrc` file with content
   ```
      {
         "root": true,
         "parser": "@typescript-eslint/parser",
         "plugins": [
            "@typescript-eslint"
         ],
         "extends": [
            "eslint:recommended",
            "plugin:@typescript-eslint/eslint-recommended",
            "plugin:@typescript-eslint/recommended"
         ]
      }
   ```
   and `.eslintignore` with content:
   ```
      node_modules
      actions

      # ignore web src if it exists
      web-src
   ```

 Visit [EsLint official site](https://eslint.org/docs/user-guide/getting-started) for more documentation.

 Add lint actions to `package.json`
 ```
    "lint": "eslint \"actions-src/**/*.{js,ts}\" ",
    "lint-fix": "eslint \"actions-src/**/*.{js,ts}\" --quiet --fix"
 ```

4. Add `tsconfig.json` file with content
   ```
   {
    "compilerOptions": {
        /* Basic Options */
        "module": "commonjs",  /*Specify module code generation: "None", "CommonJS", "AMD", "System", "UMD", "ES6", "ES2015" or "ESNext".  Only "AMD" and "System" can be used in conjunction with --outFile. "ES6" and "ES2015" values may be used when targeting "ES5" or lower.*/
        "target": "es5",  /*Specify ECMAScript target version: "ES3" (default),"ES5","ES6"/"ES2015","ES2016","ES2017","ES2018","ES2019","ES2020","ESNext"*/
        //"lib": [ "es2015", "dom" ],  /*List of library files to be included in the compilation. see https://www.typescriptlang.org/docs/handbook/compiler-options.html */
        //"removeComments": true,
        //"resolveJsonModule": true,
        //"esModuleInterop": true,
        //"typeRoots" : [
        //   "./node_modules/@types/",
        //    "./typings/"
        //],
        // "lib": [],                             /* Specify library files to be included in the compilation. */
        "allowJs": false,                       /* Allow javascript files to be compiled. */
        "checkJs": false,                       /* Report errors in .js files. */
        // "jsx": "preserve",                     /* Specify JSX code generation: 'preserve', 'react-native', or 'react'. */
        "declaration": false,                   /* Generates corresponding '.d.ts' file. */
        // "declarationMap": true,                /* Generates a sourcemap for each corresponding '.d.ts' file. */
        "sourceMap": false,                     /* Generates corresponding '.map' file. */
        // "outFile": "./",                       /* Concatenate and emit output to single file. */
        "outDir": "dist",                        /* Redirect output structure to the directory. */
        // "rootDir": "./",                       /* Specify the root directory of input files. Use to control the output directory structure with --outDir. */
        // "composite": true,                     /* Enable project compilation */
        // "removeComments": true,                /* Do not emit comments to output. */
        // "noEmit": true,                        /* Do not emit outputs. */
        //"importHelpers": true,                 /* Import emit helpers from 'tslib'. */
        // "downlevelIteration": true,            /* Provide full support for iterables in 'for-of', spread, and destructuring when targeting 'ES5' or 'ES3'. */
        // "isolatedModules": true,               /* Transpile each file as a separate module (similar to 'ts.transpileModule'). */

        /* Strict Type-Checking Options */
        //"strict": true,                           /* Enable all strict type-checking options. */
        "noImplicitAny": false,                 /* Raise error on expressions and declarations with an implied 'any' type. */
        //"strictNullChecks": false,              /* Enable strict null checks. */
        // "strictFunctionTypes": true,           /* Enable strict checking of function types. */
        // "strictPropertyInitialization": true,  /* Enable strict checking of property initialization in classes. */
        // "noImplicitThis": true,                /* Raise error on 'this' expressions with an implied 'any' type. */
        // "alwaysStrict": true,                  /* Parse in strict mode and emit "use strict" for each source file. */
        
        /* Additional Checks */
        // "noUnusedLocals": true,                /* Report errors on unused locals. */
        // "noUnusedParameters": true,            /* Report errors on unused parameters. */
        // "noImplicitReturns": true,             /* Report error when not all code paths in function return a value. */
        // "noFallthroughCasesInSwitch": true,    /* Report errors for fallthrough cases in switch statement. */
        
        /* Module Resolution Options */
        "moduleResolution": "node",            /* Specify module resolution strategy: 'node' (Node.js) or 'classic' (TypeScript pre-1.6). */
        // "baseUrl": "./",                       /* Base directory to resolve non-absolute module names. */
        // "paths": {},                           /* A series of entries which re-map imports to lookup locations relative to the 'baseUrl'. */
        // "rootDirs": [],                        /* List of root folders whose combined content represents the structure of the project at runtime. */
        // "typeRoots": [],                       /* List of folders to include type definitions from. */
        // "types": ["jest", "node"],                           /* Type declaration files to be included in compilation. */
        // "allowSyntheticDefaultImports": true,  /* Allow default imports from modules with no default export. This does not affect code emit, just typechecking. */
        "esModuleInterop": true                   /* Enables emit interoperability between CommonJS and ES Modules via creation of namespace objects for all imports. Implies 'allowSyntheticDefaultImports'. */
        // "preserveSymlinks": true,              /* Do not resolve the real path of symlinks. */
        
        /* Source Map Options */
        // "sourceRoot": "",                      /* Specify the location where debugger should locate TypeScript files instead of source locations. */
        // "mapRoot": "",                         /* Specify the location where debugger should locate map files instead of generated locations. */
        // "inlineSourceMap": true,               /* Emit a single file with source maps instead of having a separate file. */
        // "inlineSources": true,                 /* Emit the source alongside the sourcemaps within a single file; requires '--inlineSourceMap' or '--sourceMap' to be set. */
        
        /* Experimental Options */
        // "experimentalDecorators": true,        /* Enables experimental support for ES7 decorators. */
        // "emitDecoratorMetadata": true,         /* Enables experimental support for emitting type metadata for decorators. */
    },
    "include": [
        "./actions-src/**/*"
    ],
    "exclude": [
        "dev-keys"
    ]
}

5. Configure scripts that will help to build the app and compile ts code into js functions required by adobe runtime. `pre-app-run` is a command that is executed before `aio app run`. Read more about hooks [here](https://developer.adobe.com/app-builder/docs/guides/app-hooks/)
   ```
   "pre-app-run": "npm run clean && tsc",
   "clean": "shx rm -rf actions && shx echo Action Cleaning Done"
   ```


6. Add actions directory to `.gitignore`
7. Test the app: run `aio app run` and invoke the action with API.