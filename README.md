# [Any tasty ideas aka Pöpcørn](https://www.youtube.com/watch?v=B7UmUX68KtE)

## 1. TypeScript  
### 1.1. The Great Floating Transformspiler
Transform user input to proper double (float) formatting and return: first matching result / integer / given additional argument, fixed to set floating point.

```typescript
  private static getCorrectNumFormat(value: string, defaultValue: number, precision: number): string {
    // Transform user input to proper double (float) formatting and return:
    // first matching result / integer / given additional argument. For example:
    //     - "42.56.7" returns "42.56",
    //     - "....42..99.1.2.3.." returns "42.99",
    //     - ".5" returns "5"
    //     - "The Ministry of Silly Walks" returns defaultValue
    //
    // 1) (split) ------ remove any extra dots,
    // 2) (join) ------- connect with dots,
    // 3) (replace) ---- remove the dot from the left and from the right,
    // 4) (match) ------ get only the first matching substring (doubled) or digits (integrd)
    // 5) (toFixed) ---- fix to set floating point precision

    const trimmed = value.split(/\.+/).join(".").replace(/^\.|\.$/g, '');
    const doubled = trimmed.match(/[0-9]+\.[0-9]+/);
    const integrd = trimmed.match(/[0-9]+/);
    
    return Number(doubled ? doubled[0] : (integrd ? integrd[0] : defaultValue)).toFixed(precision);
  }
```

### 1.2. The Minor Pattern Validator  
Get a value from an input's event and patch scoped value or set an error if it not matched to pattern. As in example above that validation approach checks if a number format is entered.   

```typescript
  inputChange(event: any) {
    const value = event.target.value;
    if (SliderComponent.validInputPattern(value, this.formItem.itemMeta.valueType)) {
        const scoped = this.getScopedValue(value);
        this.formControl.patchValue(scoped);
    }
    else {
        this.setErrors();
    }
  }
  
  private static validInputPattern(value: string, inputType: string) {
    return Boolean(value.match(new RegExp('^\\d+(?:[.,]\\d+?)?$')));
  }
  ```
