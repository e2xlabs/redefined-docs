# Usage

## Introduction

Features include:

* The ability to find names in 3 name services at once
* Copy the address of the found domain
* And if you are a developer, then just pass a function to the props and do whatever you want with the address

## Installation

```bash
npm i @redefined/name-resolver-react
```

or download the lib from NPM registry manually:&#x20;

[https://www.npmjs.com/package/@redefined/name-resolver-react](https://www.npmjs.com/package/@redefined/name-resolver-react)

## Usage

```typescript
import React from 'react';
import { RedefinedDomainResolver } from "@redefined/name-resolver-react";

export default function App() {
  return (
    <div className="App">
        <RedefinedDomainResolver onUpdate={(address) => console.log(address)} />
    </div>
  );
}
```

To handle the user selection, pass a function to `onSelect` prop of the component.
