How to use:

```typescript
const input = {
  A: {
    B: {
      E: true;
    },
    C: {
      F: {
        G: true
      }
    },
    D: true
  }
}

findEndNodes(input) // output: [E, G, D]

```

```typescript
import { reduce } from "lodash";

type Obj = { [leaf: string]: Obj | boolean };

export const findEndNodes = (obj: Obj, accumulator?: string[] = []): string[] => {
  return reduce(
    obj,
    (acc: string[], value: Obj | boolean, key: keyof Obj) => {
      const isLeaf = typeof value === "boolean";

      if (isLeaf) {
        return [...acc, key];
      } else {
        return findEndNodes(value, acc);
      }
    },
    accumulator
  );
};
```
