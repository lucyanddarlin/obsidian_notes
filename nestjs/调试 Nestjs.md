``` json
{

  // Use IntelliSense to learn about possible attributes.

  // Hover to view descriptions of existing attributes.

  // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387

  "version": "0.2.0",

  "configurations": [

    {

      "name": "Launch via NPM",

      "type": "node",

      "request": "launch",

      "runtimeExecutable": "npm",

      "args": [

        "run",

        "start:dev",

      ],

      "skipFiles": [

        "<node_internals>/**"

      ],

      "console": "integratedTerminal"

    },

    {

      "name": "Attach",

      "port": 9229,

      "request": "attach",

      "skipFiles": [

        "<node_internals>/**"

      ],

      "type": "node"

    },

    {

      "name": "Launch Program",

      "program": "${workspaceFolder}/index.js",

      "request": "launch",

      "stopOnEntry": true,

      "skipFiles": [

        "<node_internals>/**"

      ],

      "type": "node"

    }

  ]

}
```

