---
layout: post
title: Detect duplicated list items 
description: here comes the first attempt to understand the theme
date: 2023-10-15 22:50
image: '/images/16.jpg'
tags: [code, typescript]
author: rezgar
---

**Introduction:**

I had recently to check while developing some new features, if the item is duplicated before triggering a backend request to save some time, so I wrote a generic function to check the duplication using Typescript.

**The isListPropertyDuplicated Function:**

The **`isListPropertyDuplicated`** function is a utility that allows you to determine if an array contains duplicate elements based on a specified property and a value. It has the following signature:

```jsx
public isListPropertyDuplicated<T, K extends keyof T>(
    list: T[],
    property: K,
    value: T[K]
  ): boolean {
    if (!list) {
      return false;
    }
    return list.some((listItem: T) => listItem[property] === value);
  }
```

**Usage:**

The function takes three arguments: **`list`**, **`property`**, and **`value`**. The **`list`** parameter represents the array in which duplicates will be searched. The **`property`** parameter specifies the property of the array elements to compare for duplication. Lastly, the **`value`** parameter denotes the value to compare against for duplicates.

**Example:**

Let's consider an example using an array of **`Person`** objects. Each **`Person`** object has properties like **`id`** and **`name`**. Suppose we have an array of **`people`** and want to check if there are any duplicate entries based on the **`name`** property with the value "John". We can achieve this by calling the **`isListPropertyDuplicated`** function as follows:

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

Or you can show an error message to your client and let them the duplicated property before sending the request to the Backend.

The link to the Stackblitz: [https://stackblitz-starters-fuqfgn.stackblitz.io](https://stackblitz-starters-fuqfgn.stackblitz.io/)

**Conclusion:**

The **`isListPropertyDuplicated`** function follow the software development principle(DRY: Don’t repeat yourself) , it simplifies the process of checking for duplicates within an array based on a specific property and value, it’s also generic because you can provide different data structures and not limited to one type.