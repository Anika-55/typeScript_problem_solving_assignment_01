# 📘 TypeScript Interview Questions – Blog Post (Bangla)

####1. [Interface এবং Type-এর মধ্যে পার্থক্য](#1-interface-এবং-type-এর-মধ্যে-পার্থক্য)
1.
** TypeScript-এর Interface কী?
TypeScript-এ, একটি Interface মূলত একটি সিনট্যাকটিকাল চুক্তি (syntactical contract) যা একটি অবজেক্টের প্রত্যাশিত কাঠামো নির্ধারণ করে। এটি অবজেক্টের গঠন (shape) বর্ণনা করার উপায় দেয়, যেমন তাদের প্রপার্টি এবং মেথড, তবে কোনো ফাংশনালিটি বাস্তবায়ন করে না। ইন্টারফেস শুধুমাত্র স্ট্রাকচার এবং টাইপ-চেকিং এর দিকে মনোযোগ দেয়, যা ডেভেলপমেন্টের সময় কোডের বোঝাপড়া এবং ভ্যালিডেশন উন্নত করে।

**Syntax of TypeScript Interfaces:

interface InterfaceName {
    property1: type;
    property2: type;
    // Additional properties and methods can be defined here
}

**. TypeScript-এর Typeকী?

TypeScript-এ, "type" বলতে কোনো ভ্যালুর শ্রেণীবিভাগ (classification) বোঝায়, যা তার প্রপার্টি এবং মেথডগুলি নির্ধারণ করে। TypeScript টাইপ ব্যবহার করে স্ট্যাটিক টাইপ চেকিং (static type checking) সক্ষম করে, যা ডেভেলপমেন্টের সময় রানটাইমের আগে ত্রুটি ধরতে সাহায্য করে।

**Syntax of TypeScript Type:

type Person = { name: string };
type Employee = Person & { salary: number };

**🔹 2. Declaration Merging (ঘোষণা একত্র করা)
#Interface supports merging
interface User { name: string; }
interface User { age: number; }
// Merged result: { name: string; age: number; }


##Type does NOT support merging

type User = { name: string };
type User = { age: number }; // ❌ Error

**🔹 3. Flexibility

Type alias বেশি flexible:

* primitive
* union
* tuple
* function signatures সবকিছুতে ব্যবহার করা যায়।
Example:
type ID = number | string;
type Position = [number, number];

Interface →“ইমপ্লিমেন্ট করার মতো” → অবজেক্ট/ক্লাসের কাঠামোর জন্য।

Type → “ট্রিকস্টার” → যেকোনো টাইপ (ইউনিয়ন, টুপল, অবজেক্ট, প্রিমিটিভ) সংজ্ঞায়নের জন্য ফ্লেক্সিবল।


###2.What is the use of the keyof keyword in TypeScript?

TypeScript-এ keyof কীওয়ার্ড ব্যবহার করা হয় কোনো অবজেক্ট টাইপের সব key-এর ইউনিয়ন টাইপ পাওয়ার জন্য। অর্থাৎ, এটি আমাদের দেয় সেই অবজেক্টে থাকা property গুলোর নামের টাইপ।

ব্যবহার :

1.টাইপ-সেফ অ্যাকসেস: নিশ্চিত করে আপনি কেবল সেই প্রপার্টিগুলো ব্যবহার করছেন যা অবজেক্টে সত্যিই আছে।

2.ডাইনামিক কিন্তু সেফ প্রোগ্রামিং: যখন key গুলো hardcode না করে ব্যবহার করতে চান, তখন টাইপ সেফ উপায় দেয়।

3.Generics এবং Utility Types: জেনেরিক ফাংশন বা টাইপ তৈরিতে ব্যবহার করা হয়, যাতে ফাংশনগুলো অবজেক্টের key অনুযায়ী কাজ করে।
Example:

interface Person {
  name: string;
  age: number;
  city: string;
}

// keyof ব্যবহার করে সব key-এর টাইপ পাওয়া
type PersonKeys = keyof Person;  
// PersonKeys এখন হবে: "name" | "age" | "city"

// key টাইপ ব্যবহার করে টাইপ-সেফ ফাংশন
function getValue(obj: Person, key: PersonKeys) {
  return obj[key];
}

const person: Person = { name: "Alice", age: 28, city: "Dhake" };

console.log(getValue(person, "name")); // ঠিক আছে
console.log(getValue(person, "age"));  // ঠিক আছে
// console.log(getValue(person, "country")); // ❌ error, country নেই











