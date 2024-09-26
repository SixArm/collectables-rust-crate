# Collectables: Rust crate of collections helpers

This `collectables` Rust crate provides helpers 
for BTreeMap, BTreeSet, HashMapSet, etc. By SixArm.com.

This crate provides two general-purpose collections helpers:

* BTreeMapToSet<K, V> is based on BTreeMap<K, BTreeSet<V>>

* HashMapToSet<K, V> is based on HashMap<K, HashSet<V>>


## Examples

Example that maps a word to a set of other words:

```rust
// Use this crate
use collectables::*;

// Create an empty hash map, where each vaue is a hash set.
let mut a: HashMapToSet<String, String> = HashMapToSet::new();

/// Create some example strings
let hello   = String::from("hello");   // English example
let ninhao  = String::from("nǐn hǎo"); // Chinese example
let hola    = String::from("hola");    // Spanish example

// Insert items, such as mapping the word "hello" to various tranlations.
// The first parameter is a map key; the second parameter is a set item.
a.sub_insert(hello.to_string(), ninhao.to_string());
a.sub_insert(hello.to_string(), hola.to_string());

// Does the collection contain a word map key to a word set item?
assert_eq!(a.sub_contains(&hello, &ninhao), true);

// Remove an item from the map key set.
a.sub_remove(&hello, &ninhao);

// These collections helpers are implemented as trait extensions,
// thus all HashMap functions and HashSet functions are available,
// and can be intermixed with the HashMapSet trait extensions.
assert_eq!(a.get(&hello).unwrap().contains(&hola), true);
```

## Specific-purpose collections helpers

This crate provides two specific-purpose collections helpers:

* BTreeMapOfFileLenToSetOfPathBuf is based on BTreeMap<u64, BTreeSet<PathBuf>>

* HashMapOfFileLenToSetOfPathBuf is based on HashMap<u64, HashSet<PathBuf>>

The helpers are implemented as trait extensions i.e. the helpers add 
functions to existing Rust std::collections code.

```rust
// Use this crate
use collectables::*;

// Create a path to an existing file 
let alpha = std::path::PathBuf::from("alpha.txt");

// Create a collection to map the file length to a set of path buffers.
let mut a: HashMapOfFileLenToSetOfPathBuf = HashMapOfFileLenToSetOfPathBuf::new();

// Insert the path, which uses the path metadata file length as a map key.
a.sub_insert_path(alpha.clone());

// Does the collection contain a path?
assert_eq!(a.sub_contains_path(&alpha), true);

// Remove an item from the map key set
a.sub_remove_path(alpha.clone());
```


## Tracking

Contact: Joel Parker Henderson <joel@joelparkerhenderson.com>

License: MIT or Apache-2.0 or GPL-2.0-only
