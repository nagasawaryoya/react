[![NodeCI](https://github.com/ts-graphviz/react/workflows/NodeCI/badge.svg)](https://github.com/kamiazya/ts-graphviz/actions?workflow=NodeCI) [![npm version](https://badge.fury.io/js/%40ts-graphviz%2Freact.svg)](https://badge.fury.io/js/%40ts-graphviz%2Freact) [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT) [![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com) [![tested with jest](https://img.shields.io/badge/tested_with-jest-99424f.svg)](https://github.com/facebook/jest) [![code style: prettier](https://img.shields.io/badge/code_style-prettier-ff69b4.svg)](https://github.com/prettier/prettier)

# @ts-graphviz/react

Graphviz-dot Renderer using React.

## Installation

The module can then be installed using [npm](https://www.npmjs.com/):

[![NPM](https://nodei.co/npm/@ts-graphviz/react.png)](https://nodei.co/npm/@ts-graphviz/react/)

```bash
# yarn
$ yarn add @ts-graphviz/react
# or npm
$ npm install @ts-graphviz/react
```

### Peer Dependencies

- [React and ReactDOM](https://github.com/facebook/react/)(>=16.8)
- [ts-graphviz](https://github.com/ts-graphviz/ts-graphviz)
- [@hpcc-js/wasm](https://www.npmjs.com/package/@hpcc-js/wasm) (Optional)

```bash
# Peer Dependencies
$ yarn add react react-dom ts-graphviz@"^0.13.1"
```

## API

### Script

```tsx
import React, { FC } from 'react';
import { Digraph, Node, Subgraph, Edge, DOT, renderToDot } from '@ts-graphviz/react';

const Example: FC = () => (
  <Digraph
    rankdir="TB"
    edge={{
      color: 'blue',
      fontcolor: 'blue',
    }}
    node={{
      shape: 'none',
    }}
  >
    <Node
      id="nodeA"
      shape="none"
      label={
        <DOT.TABLE BORDER="0" CELLBORDER="1" CELLSPACING="0">
          <DOT.TR>
            <DOT.TD>left</DOT.TD>
            <DOT.TD PORT="m">middle</DOT.TD>
            <DOT.TD PORT="r">right</DOT.TD>
          </DOT.TR>
        </DOT.TABLE>
      }
    />

    <Subgraph id="cluster" label="Cluster" labeljust="l">
      <Node id="nodeB" label="This is label for nodeB." />
    </Subgraph>
    <Edge targets={['nodeB', 'nodeA:m']} comment="Edge from node A to B" label={<DOT.B>A to B</DOT.B>} />
  </Digraph>
);

const dot = renderToDot(<Example />);

console.log(dot);
```

### Output dot

```dot
digraph {
  rankdir = "TB";
  edge [
    color = "blue",
    fontcolor = "blue",
  ];
  node [
    shape = "none",
  ];
  "nodeA" [
    shape = "none",
    label = <<TABLE BORDER="0" CELLBORDER="1" CELLSPACING="0"><TR><TD>left</TD><TD PORT="m">middle</TD><TD PORT="r">right</TD></TR></TABLE>>,
  ];
  subgraph "cluster" {
    labeljust = "l";
    label = "Cluster";
    "nodeB" [
      label = "This is label for nodeB.",
    ];
  }
  // Edge from node A to B
  "nodeB" -> "nodeA":"m" [
    label = <<B>A to B</B>>,
  ];
}
```

![dot](./example/example.svg)

## See Also

Graphviz-dot Test and Integration

- [ts-graphviz](https://github.com/ts-graphviz/ts-graphviz)
  - Graphviz library for TypeScript.
- [jest-graphviz](https://github.com/ts-graphviz/jest-graphviz)
  - Jest matchers that supports graphviz integration.
- [setup-graphviz](https://github.com/ts-graphviz/setup-graphviz)
  - GitHub Action to set up Graphviz cross-platform(Linux, macOS, Windows).

## License

This software is released under the MIT License, see [LICENSE](./LICENSE).
