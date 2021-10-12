input:
```typescript
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
```

output:
```typescript
[E, G, D]
```


```typescript
import { reduce } from "lodash";

type Obj = { [leaf: string]: Obj | boolean };

export const findEndNodes = (
  accumulator: string[] = [],
  obj: Obj = {}
): string[] => {
  return reduce(
    obj,
    (acc: string[], value: Obj | boolean, key: keyof Obj) => {
      const isLeaf = typeof value === "boolean";

      if (isLeaf) {
        return [...acc, key];
      } else {
        return findEndNodes(acc, value);
      }
    },
    accumulator
  );
};
```
