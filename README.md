# [Any tasty ideas aka Pöpcørn](https://www.youtube.com/watch?v=B7UmUX68KtE)

## 1. TypeScript  
### 1.1. The Great Floating Transformspiler
Transform user input to proper double (float) formatting and return: first matching result / integer / given additional argument.

```typescript
  private static getCorrectDouble(value: string, defaultValue: string): string {
    // Transform user input to proper double (float) formatting and return:
    // first matching result / integer / given additional argument. For example:
    //     - "42.56.7" returns "42.56",
    //     - "....42..99.1.2.3.." returns "42.99",
    //     - ".5" returns "5"
    //     - "The Ministry of Silly Walks" returns minValue
    //
    // 1) (split) ---- remove any extra dots,
    // 2) (join) ----- connect with dots,
    // 3) (replace) -- remove the dot from the left and from the right,
    // 4) (match) ---- get only the first matching substring (doubled) or digits (integrd)

    const trimmed = value.split(/\.+/).join(".").replace(/^\.|\.$/g, '');
    const doubled = trimmed.match(/[0-9]+\.[0-9]+/);
    const integrd = trimmed.match(/[0-9]+/);

    return doubled ? doubled[0] : (integrd ? integrd[0] : defaultValue);
  }
```
