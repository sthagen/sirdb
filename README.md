# :card_file_box: [stubdb](https://github.com/crislin2046/stubdb) ![npm downloads](https://img.shields.io/npm/dt/stubdb) ![version](https://img.shields.io/npm/v/stubdb?label=version)

A very simple "database" on the file system for when you're too small to fail.

## api

There's only 5 calls in this api: `config`, `dropTable`, `getTable`, `put`, `get`

See below for how they're used:

```javascript
  const root = path.resolve(__dirname, "test-get-table");
  let gotItems;
  let key = 1;

  config({root});

  dropTable("items");

  const Items = getTable("items");
  const items = [
    {
      key: `key${key++}`,
      name: 'Apple',
      type: 'fruit',
      grams: 325
    },
    {
      key: `key${key++}`,
      name: 'Pear',
      type: 'fruit',
      grams: 410
    },
    {
      key: `key${key++}`,
      name: 'Soledado',
      type: 'career',
      grams: null,
      qualities_of_winners: [
        "devisiveness",
        "rationality",
        "aggression",
        "calmness"
      ]
    },
  ];
  
  try {
    items.forEach(item => Items.put(item.key, item));
  } catch(e) {
    errors.push(e);
  }

  assert.strictEqual(errors.length, 0);

  try {
    gotItems = items.map(item => Items.get(item.key));
  } catch(e) {
    errors.push(e);
  }

  assert.strictEqual(errors.length, 0);
  
  try {
    Items.get("no such key");
  } catch(e) {
    // we will always throw
  }

  assert.strictEqual(JSON.stringify(items), JSON.stringify(gotItems));
  ```

------------

# *Stub It!*

