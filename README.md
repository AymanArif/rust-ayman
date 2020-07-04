# Rust talks



# [Traits and You: A Deep Dive — Nell Shamrell-Harrington](https://www.youtube.com/watch?v=grU-4u0Okto) 


## 101 - Intro to Traits


- Structs
Structs allows to create stuff in appropriate group


```rust
struct Dwarf {
   name: String
}
struct Elf {
   name: String
}
``` 

// Create defintion for your struct

let lotr_dwarf = Dwarf { name: String::from("NauAlMuq") };

- Trait

pub trait Armour {
   fn armour_cost(&self) -> u8;
}

- Now implement Trait

```rust
impl Armour for Dwarf {
   fn armour_cost(&self) -> u8 {
       2
   }
}
let lotr_dwarf = Dwarf { name: String::from("NauAlMuq") };
lotr_dwarf.armour_cost() // 2
```

- Default Value

```rust
pub trait Armour {
   fn armour_cost(&self) -> u8 {
     0
   }
}
impl Armour for Sauran {
}
impl Armour for Gandalf {
}
let lotr_sauran = Sauran { name: String::from("NauAlMuq") };
lotr_sauran.armour_cost() // Default: 0
```


## 201 - Trait Bounds



```rust


pub trait English {
   
}

// Now implement Trait

impl English for Dwarf {
}

pub fn<T:English>(character:T) -> String { 
  // (character:T) : Accept any of type T
  // (T:English)   : Only accept trait which implements English
  String::from("yes") 
}

let lotr_dwarf = Dwarf { name: String::from("NauAlMuq") };
speak_english(lotr_dwarf) // 2

let lotr_sauran = Sauran { name: String::from("NauAlMuq") };
speak_english(lotr_sauran)
// Compiler error
// Trait "English" is not implemented for Sauran

```

> Allow function to ony accept **traits** that **implement** a certain **trait**


## 301 - Trait Objects

Traditional OOP:
**Object = Data + Behaviour**

Rust:

**Enum/Structs = Data**
**Behaviour = Trait**


**Trait Object = Tradition Object = Data(Pointer to a value in Heap) + Behaviour (Trait)**
Cannot add data to trait object


## Code

Ring is god. 

struct Invisble {

}

struct Strength{
}

pub trait Cast {
 fn cast (&self);
}

impl Cast for Invisible {
 fn cast (&self){ ... Details ... }
}

impl Cast for Strength {
 fn Cast (&self){ ... Details ... }
}

struct SpellBook {
  pub spells: Vec<Box<Cast>>,
  // Vector : Group of objects of specific type. Here it is box
  // Box: Pointer to a value in the heap
  // Cast: A trait. Here Box points to Cast trait
}

impl SpellBook {
  pub fn run (&self) {
    for spell in self.spells.iter() { spell.cast(); //fn cast (&self){ ... Details ... } }
  }
}


let spell_book = SpellBook {
		spells:vec![
		  Box::new(Strength{})
                  Box::new(Invisible{})
		],
		};
spell_book.run(); 


Trait Objects are great for heteregenous collections.






