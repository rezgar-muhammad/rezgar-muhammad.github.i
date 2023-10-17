---
layout: post
title: How to detect duplicate items in a list
description: a genric function to detect duplicate item in a list using Typescript
date: 2023-10-16 20:00
image: '/images/blake-wheeler.jpg'
tags: [code, typescript]
author: rezgar
---
**Introduction:**

I had recently to check while developing some new features, if the item is duplicated in an array of complex objects before triggering a backend request to save some time, so I wrote a generic function to check the duplication using Typescript.

**The isListPropertyDuplicated Function:**

The **`isListPropertyDuplicated`** function is a utility that allows you to determine if an array contains duplicate elements based on a specified property and a value. It has the following signature:

```jsx
public isListPropertyDuplicated<T, K extends keyof T>(
    list: T[],
    property: K,
    value: T[K]
  ): boolean {
    if (!list || list.length === 0) {
      return false;
    }
    return list.some((listItem: T) => listItem[property] === value);
  }
```

**Usage:**

The function takes three arguments: **`list`**, **`property`**, and **`value`**. The **`list`** parameter represents the array in which duplicates will be searched. The **`property`** parameter specifies the property of the array elements to compare for duplication. Lastly, the **`value`** parameter denotes the value to compare against for duplicates.

**Example:**

Let's consider an example using an array of **`Person`** objects. Each **`Person`** object has properties like **`id`** and **`name`**. Suppose we have an array of **`people`** and want to check if there are any duplicate entries based on the **`name`** property with the value "John". We can achieve this by calling the **`isListPropertyDuplicated`** function as following:

```jsx
const people: Person[] = [
  { id: 1, name: "Bob" },
  { id: 2, name: "John" },
  { id: 3, name: "Bob" },
];

const hasDuplicateItem = isListPropertyDuplicated(people, "name", "Bob");
console.log(hasDuplicateItem); // Output: true
```

In this example, the function efficiently searches the **`people`** array for duplicate **`name`** values and returns **`true`** if any duplicates are found.

Now we have this info, if our array contains duplicated items, usually you are also interested in removing the duplicating items, I will write another article on how we can remove them in a generic way for both `primitive and complex Objects`

Or you can show an error message to your client and let them know the duplicated property before sending the request to the Backend.

The link to the Stackblitz: [is List Item duplicated](https://stackblitz.com/edit/islistitemduplicated?file=src%2Fmain.ts,src%2FhelperService.ts)

**Conclusion:**

The **`isListPropertyDuplicated`** function follow the software development principle(DRY: Don’t repeat yourself) , it simplifies the process of checking for duplicates within an array based on a specific property and value, it’s also generic because you can provide different data structures and not limited to one type.