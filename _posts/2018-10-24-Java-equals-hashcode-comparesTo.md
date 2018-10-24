---
title: "Java Overrides equals(), hashCode(), compareTo()"
layout: post
date: 2018-10-24
# image: /assets/images/adsk.JPG
headerImage: false
tag:
- markdown
- components
- extra
category: blog
author: YY
description: Markdown summary with different options
---

## Two rule when dealing with object identification in Java
1. Override hashCode when you override equals
2. Make conpareTo consistent with euqals

## Default equals is based on memory location of two objects, so we need to customize it to meet our need.
1. equals must conform to rules: 
    * x.equals(x)
    * x.equals(y) then must y.equals(x)
    * x.equals(y) and y.equals(z) then x.equals(z)
    * mutiple invocations of x.equals(y) return same
    * if x is not null, x.equals(null) return false
2. Five-step for overridding equals()
``` 
    public class SampleEquals {
        private int val1;
        private int val2;
        ...

        public boolean equals (Object o) {
            //step 1: check if o is current object (== checks addresses in memory)
            if（this == o）{
                return true;
            }

            // step 2: instance check
            if (!(o instanceof SampleEquals)) {
                return false;
            }

            // step 3: cast
            SampleEquals other = (SampleEquals) o;

            // step 4: customized check
            return other.val1 == this.val1 && other.val2 == this.val2;

            // step 5: checks all the rules for equals() above
        }
    }
```

## hashCode() method of objects is used when you insert them into a HashTable, HashMap or HashSet. 
* When these data structure need to compare two objects, first they compare their hash codes, if they have same hash codes, then compare use equals. 
* Default hashCode() hashes addresses of object. 
* How HashTable get() works with hashCode()
    * hashCode() gets key's hash code
    * retrieve the list of pairs stored in the bucket
    * scan through each entry until one key equals() current key
* Two ways of generate customized hash code
    * concatenate all fields into a string, and return hashed value
    * add each field's hash code together
        ```
            public class SampleHashCode {
                private int val1;
                private int val2;
                ...
                public int hashCode1() {
                    int hash1 = Object.hashCode("" + val1 + val2);
                    return hash1;
                }

                public int hashCode2() {
                    int hash2 = Object.hashCode(val1) + Object.hashCode(val2);
                    return hash2;
                }
            }
        ```   

## compareTo() is used to implement natural sorting on Java classes
* rules of compareTo()
    * returns negative integer means less than
    * returns 0 means equal
    * returns positive integer means greater than
* costomize compareTo() by specifying how we want to order
```
    public class SampleCompareTo {
        private final Strint name;
        private final int id;
        ...
        public int compareTo(SampleCompareTo o) {
            int res = this.name.compareTo(o.name);
            if (res == 0) {
                res = Integer.valueOf(this.id).compareTo(o.id); 
            }
            return res;
        }
    }
```
