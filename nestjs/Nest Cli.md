项目开发离不开工程化的部分，比如创建项目，编译构建等等:
``` sh
npx nest new project_name
```
或
```sh
npm install -g @nestjs/cli

nest new project_name

#sometime
npm update -g @nestjs/cli
```

查看一下 Nest Cli 提供哪些指令:
```sh
# nest -h

Usage: nest <command> [options]

Options:
  -v, --version                                   Output the current version.
  -h, --help                                      Output usage information.

Commands:
  new|n [options] [name]                          Generate Nest application.
  build [options] [app]                           Build Nest application.
  start [options] [app]                           Run Nest application.
  info|i                                          Display Nest project details.
  add [options] <library>                         Adds support for an external library to your project.
  generate|g [options] <schematic> [name] [path]  Generate a Nest element.
    Schematics available on @nestjs/schematics collection:
      ┌───────────────┬─────────────┬──────────────────────────────────────────────┐
      │ name          │ alias       │ description                                  │
      │ application   │ application │ Generate a new application workspace         │
      │ class         │ cl          │ Generate a new class                         │
      │ configuration │ config      │ Generate a CLI configuration file            │
      │ controller    │ co          │ Generate a controller declaration            │
      │ decorator     │ d           │ Generate a custom decorator                  │
      │ filter        │ f           │ Generate a filter declaration                │
      │ gateway       │ ga          │ Generate a gateway declaration               │
      │ guard         │ gu          │ Generate a guard declaration                 │
      │ interceptor   │ itc         │ Generate an interceptor declaration          │
      │ interface     │ itf         │ Generate an interface                        │
      │ library       │ lib         │ Generate a new library within a monorepo     │
      │ middleware    │ mi          │ Generate a middleware declaration            │
      │ module        │ mo          │ Generate a module declaration                │
      │ pipe          │ pi          │ Generate a pipe declaration                  │
      │ provider      │ pr          │ Generate a provider declaration              │
      │ resolver      │ r           │ Generate a GraphQL resolver declaration      │
      │ resource      │ res         │ Generate a new CRUD resource                 │
      │ service       │ s           │ Generate a service declaration               │
      │ sub-app       │ app         │ Generate a new application within a monorepo │
      └───────────────┴─────────────┴──────────────────────────────────────────────┘
```

### nest new
```sh
# nest new -h
Usage: nest new|n [options] [name]

Generate Nest application.

Options:
  --directory [directory]                 Specify the destination directory
  -d, --dry-run                           Report actions that would be performed without writing out results. (default: false)
  -g, --skip-git                          Skip git repository initialization. (default: false)
  -s, --skip-install                      Skip package installation. (default: false)
  -p, --package-manager [packageManager]  Specify package manager.
  -l, --language [language]               Programming language to be used (TypeScript or JavaScript) (default: "TypeScript")
  -c, --collection [collectionName]       Schematics collection to use (default: "@nestjs/schematics")
  --strict                                Enables strict mode in TypeScript. (default: false)
  -h, --help                              Output usage information.
```

- --skip-git 和 --skip-install 就是跳过 git 的初始化和跳过 npm install
- --package-manager 是指定包管理器, 输入`nest new project_name -p pnpm` 就能完成指定

### nest generate
nest cli 命令除了可以生成整个项目之外，还可以生成一些别的代码块，比如 `controller`, `service`, `module`:
像 `nest generate module your_moudle_name`, 它会生成 module 部分的代码，同时也会在 AppModule 中导入。生成 `controller`, `service` 也同理

更多:
```sh
Usage: nest generate|g [options] <schematic> [name] [path]

Generate a Nest element.
  Schematics available on @nestjs/schematics collection:
    ┌───────────────┬─────────────┬──────────────────────────────────────────────┐
    │ name          │ alias       │ description                                  │
    │ application   │ application │ Generate a new application workspace         │
    │ class         │ cl          │ Generate a new class                         │
    │ configuration │ config      │ Generate a CLI configuration file            │
    │ controller    │ co          │ Generate a controller declaration            │
    │ decorator     │ d           │ Generate a custom decorator                  │
    │ filter        │ f           │ Generate a filter declaration                │
    │ gateway       │ ga          │ Generate a gateway declaration               │
    │ guard         │ gu          │ Generate a guard declaration                 │
    │ interceptor   │ itc         │ Generate an interceptor declaration          │
    │ interface     │ itf         │ Generate an interface                        │
    │ library       │ lib         │ Generate a new library within a monorepo     │
    │ middleware    │ mi          │ Generate a middleware declaration            │
    │ module        │ mo          │ Generate a module declaration                │
    │ pipe          │ pi          │ Generate a pipe declaration                  │
    │ provider      │ pr          │ Generate a provider declaration              │
    │ resolver      │ r           │ Generate a GraphQL resolver declaration      │
    │ resource      │ res         │ Generate a new CRUD resource                 │
    │ service       │ s           │ Generate a service declaration               │
    │ sub-app       │ app         │ Generate a new application within a monorepo │
    └───────────────┴─────────────┴──────────────────────────────────────────────┘
```
如果是要完整生成一个模块的代码，那么不需要一个个生成，直接输入 `nest generate resource xxxx` 即可生成，同样地也会注册到 AppModule 中。

### nest start 
```sh
❯ nest start -h
Usage: nest start [options] [app]

Run Nest application.

Options:
  -c, --config [path]        Path to nest-cli configuration file.
  -p, --path [path]          Path to tsconfig file.
  -w, --watch                Run in watch mode (live-reload).
  -b, --builder [name]       Builder to be used (tsc, webpack, swc).
  --watchAssets              Watch non-ts (e.g., .graphql) files mode.
  -d, --debug [hostport]     Run in debug mode (with --inspect flag).
  --webpack                  Use webpack for compilation (deprecated option, use --build instead).
  --webpackPath [path]       Path to webpack configuration.
  --type-check               Enable type checking (when SWC is used).
  --tsc                      Use tsc for compilation.
  --sourceRoot [sourceRoot]  Points at the root of the source code for the single project in standard mode structures,
                             or the default project in monorepo mode structures.
  --entryFile [entryFile]    Path to the entry file where this command will work with. Defaults to the one defined at
                             your Nest's CLI config file.
  -e, --exec [binary]        Binary to run (default: "node").
  --preserveWatchOutput      Use "preserveWatchOutput" option when tsc watch mode.
  -h, --help                 Output usage information.
```

### 总结
Nest Cli 提供了很多快捷的命令，用于生成、调试、编译代码。