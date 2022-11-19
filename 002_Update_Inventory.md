## Update Inventory
Compare and update the inventory stored in a 2D array against a second 2D array of a fresh delivery. Update the current existing inventory item quantities (in arr1). If an item cannot be found, add the new item and quantity into the inventory array. The returned inventory array should be in alphabetical order by item.
## Solution
###### Flatten the 2D array of inventory into arrays of quantities and items with the same length.
```
function getQuantity(arr) {
    const quantities = arr.map(item => item[0]);
    return quantities;
}

function getItem(arr) {
    const items = arr.map(item => item[1])
    return items;
}
```
###### The main function to update inventory
```
function updateInventory(arr1, arr2) {
    const curInventoryQuantities = getQuantity(arr1)
    //console.log('cur quantities', curInventoryQuantities)
    const curInventoryItems = getItem(arr1)
    //console.log('cur inventory items', curInventoryItems)

    const deliveryQuantities = getQuantity(arr2);
    //console.log('delivery quantities', deliveryQuantities)
    const deliveryItems = getItem(arr2);
    //console.log('delivery items', deliveryItems)

    for (let i in deliveryItems) {
        const deliveryItem = deliveryItems[i]
        const deliveryQuantity = deliveryQuantities[i]
        //console.log('delivery item', deliveryItem)
        //console.log('delivery Quantity', deliveryQuantity)

        const indexInventory = curInventoryItems.indexOf(deliveryItem);
        //console.log('index of inventory', indexInventory)
        if (indexInventory === -1) {
            curInventoryItems.push(deliveryItem);
            curInventoryQuantities.push(deliveryQuantity)
        } else {
            curInventoryQuantities[indexInventory] += deliveryQuantity;
        }
    }

    //console.log(`update inventory items is ${curInventoryItems}, update inventory quantities are ${curInventoryQuantities}`)
    const updateInventoryArray = curInventoryItems.reduce(function (allInventory, item, index) {
        allInventory.push([curInventoryQuantities[index], item])
        return allInventory;
    }, [])
    //sort by inventory items
    updateInventoryArray.sort((a, b) => {
        const nameA = a[1].toUpperCase(); // ignore upper and lowercase
        const nameB = b[1].toUpperCase(); // ignore upper and lowercase
        if (nameA < nameB) {
            return -1;
        }
        if (nameA > nameB) {
            return 1;
        }
        // names must be equal
        return 0;
    });
    //console.log('update inventory', updateInventoryArray)
    return updateInventoryArray;
}
```
## Takeaway notes
- Console.log is powerful
- Flatten mutiple dimensions into one dimension array could help easing the problem.
