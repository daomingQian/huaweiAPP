const arr = [
  { id: 56, parentId: 62 },
  { id: 81, parentId: 80 },
  { id: 74, parentId: null },
  { id: 76, parentId: 80 },
  { id: 63, parentId: 62 },
  { id: 80, parentId: 86 },
  { id: 87, parentId: 86 },
  { id: 62, parentId: 74 },
  { id: 86, parentId: 74 },
];

function arrTotree(arr) {
  const idMapping = arr.reduce((accumulator, currentValue, index) => {
    accumulator[currentValue.id] = index;
    return accumulator
  }, {})

  let root = null;
  arr.forEach(el => {
    if (!el.parentId) {
      root = el;
    } else {
      const parentEl = arr[idMapping[el.parentId]];
      parentEl.children = [...(parentEl.children || []), el];
    }
  })
  return root
}

function treeToarr(tree) {
  let arr = [];
  arr.push({ id: tree.id, parentId: tree.parentId })
  let childrens = tree.children;

  while (childrens.length) {
    let newChildrens = [];
    childrens.forEach(item => {
      arr.push({ id: item.id, parentId: item.parentId });
      newChildrens.push(...(item.children || []));
    })
    childrens = newChildrens;
  }
  return arr;
}

treeToarr(arrTotree(arr));



