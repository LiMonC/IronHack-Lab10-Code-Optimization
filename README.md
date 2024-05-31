# IronHack-Lab10-Code-Optimization
# Code Optimization Practice

### Objective:
Enhance the performance of provided code snippets by applying code-level optimization techniques manually. This lab focuses on deepening your understanding and application of optimization principles in coding.


### Instructions:

* At the beginning of the lab, you will receive a set of code snippets that contain common performance issues. These snippets will come from different programming languages, including JavaScript, Java, and C#, to cover a variety of scenarios and common inefficiencies found in real-world programming.

### Provided Code Snippets:

##### JavaScript Snippet:
``` javascript
// Inefficient loop handling and excessive DOM manipulation
function updateList(items) {
  let list = document.getElementById("itemList");
  list.innerHTML = "";
  for (let i = 0; i < items.length; i++) {
    let listItem = document.createElement("li");
    listItem.innerHTML = items[i];
    list.appendChild(listItem);
  }
}
```
##### Analysis:

*  **Inefficient Loop handling**:


*  **Excessive DOM manipulation**:
      * In each loop a call is made to go to the DOM, constantly accessing and manipulating the DOM can result in a poor performance (and user experience), particularly when the number of elements becomes very large.

    
##### Optimization:
```javascript


function updateList(items) {
    let list = document.getElementById("itemList");
    const fragment = document.createDocumentFragment();
    items.forEach((_, i) => {
        const listItem = document.createElement("li");
        listItem.innerHTML =  items[i];
        fragment.appendChild(listItem);
    });
    document.body.appendChild(fragment);
}
```

##### Explanation:

1.  **Preinitialize a `fragment`**:

    -   By initializing `fragment`  we can handle in memory the new generated items
      
2.  **Using a `forech` Loop**:

    -   Using a forEach loopwe don't have to index in every time.
      
3.  **add FragmentView into general DOM**:

    -   Interact only one time with the DOM.

___

##### Java Snippet:

``` java
// Redundant database queries
public class ProductLoader {
    public List<Product> loadProducts() {
        List<Product> products = new ArrayList<>();
        for (int id = 1; id <= 100; id++) {
            products.add(database.getProductById(id));
        }
        return products;
    }
}
```

###### Analysis:

*  **Inefficient Loops**:
* **Redundant and Unoptimized Database Queries**:

###### Optimization:

``` java

public class ProductLoader {
    public List<Product> loadProducts(from, to) {
        return database.getProductsById(from, to); 
    }
}

// Usage
loadProducts(0,100)
```

###### Explanation:

*  **Single Query to load All Products**:
*  **Simple Loop**: streamlining loops to reduce computational overhead.
*  **Optimized Database Queries**: Enhancing database queries to reduce load times.

___

##### C# Snippet:

```csharp
// Unnecessary computations in data processing
public List<int> ProcessData(List<int> data) {
    List<int> result = new List<int>();
    foreach (var d in data) {
        if (d % 2 == 0) {
            result.Add(d * 2);
        } else {
            result.Add(d * 3);
        }
    }
    return result;
}
```

###### Analysis:

*  **Inefficient Loops**:
*  **Redundant Computations**:
*  **Excessive Memory Usage**:
*  **Unoptimized Data Processing**:

###### Optimization:

``` csharp
public List<int> ProcessData(List<int> data) {
    var result = new ConcurrentBag<int>();
    Parallel.ForEach(data, d => 
    {
        int value = d % 2 == 0 ? d * 2 : d * 3;
        result.Add(value);
    });

    return result.ToList();
}

```
###### Explanation:

*  **Streamlining loops to reduce computational overhead.**:
*  **Harnessing Concurrency in Loops:**: with the use of `ConcurrentBag` we can allow generic data to be stored in the unordered form. It allows to store duplicate objects.
*  **Reducing complexity by improving conditional logic** we can improve the use of the conditional logic by simplifying the code with the ternary operator: `int value = d % 2 == 0 ? d * 2 : d * 3;`

