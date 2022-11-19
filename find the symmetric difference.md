## Find the Symmetric Difference
The mathematical term symmetric difference (△ or ⊕) of two sets is the set of elements which are in either of the two sets but not in both. For example, for sets A = {1, 2, 3} and B = {2, 3, 4}, A △ B = {1, 4}.
Symmetric difference is a binary operation, which means it operates on only two elements. So to evaluate an expression involving symmetric differences among three elements (A △ B △ C), you must complete one operation at a time. Thus, for sets A and B above, and C = {2, 3}, A △ B △ C = (A △ B) △ C = {1, 4} △ {2, 3} = {1, 2, 3, 4}.
###### Create a function that takes two or more arrays and returns an array of their symmetric difference. The returned array must contain only unique values (no duplicates).
## Solution
###### Find the common of two arrays
```
function joinOfTwo(arr1, arr2) {
  const joinArr = [];
  for (let e of arr1) {
    if (arr2.indexOf(e) > -1) {
      joinArr.push(e)
    }
  }
  return joinArr;
};
```
###### Find the difference of two arrays
```
function difOfTwo(arr1, arr2) {
  const joinArr = joinOfTwo(arr1, arr2);
  const joinOuter = [...arr1, ...arr2];

  const difArr = [];
  for (let e of joinOuter) {
    if (joinArr.indexOf(e) === -1 && difArr.indexOf(e) === -1) {
      difArr.push(e)
    }
  }
  return difArr;
}
```
###### A function receives two or more than two arrays and return the symmetric difference.
```
function sym(arr1, arr2,...args) {
  const len = args.length;
  let dif = difOfTwo(arr1, arr2);
  for (let i = 0; i < len; i++) {
    const newDif = difOfTwo(dif, args[i])
    dif = newDif; //assign dif with the newDif
  }
  dif.sort();
  return dif;
};
```
## Takeaway notes
- Use a rest parameter to collect all arguments after the first two parameters.
- Can convert a problem with multiple variables to a problem with two variables.
- Reverse thinking could help!
