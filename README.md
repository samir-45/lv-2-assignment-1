# **Blog 1: TypeScript এ Interface আর Type এর পার্থক্য**

TypeScript-এ object এর গঠন বোঝাতে আমরা `interface` আর `type` দুটোই ব্যবহার করি। অনেক জায়গায় দুটো একই রকম লাগে, কিন্তু কিছু গুরুত্বপূর্ণ পার্থক্য আছে।

**Interface** মূলত object structure বর্ণনা করার জন্য। এটাকে বারবার declare করলে TypeScript অটো merge করে ফেলে।
যেমন:

```ts
interface User { name: string }
interface User { age: number }
// এখন User এর ভিতরে name + age দুটোই থাকবে


**Type** আরও flexible — union, tuple, function type সব কিছুর জন্য ব্যবহার করা যায়। কিন্তু type দুইবার declare করলে error আসে এবং merge হয় না।


# **Blog 2: keyof কীওয়ার্ড কী এবং কেন দরকার?**

`keyof` এমন একটি keyword যা কোনো object type এর সব key গুলোকে একটি union আকারে বের করে দেয়। এটা তখন কাজে লাগে যখন আমরা এমন function বানাতে চাই যেটা valid key ছাড়া অন্য কিছু নিতে পারবে না। এতে কোড আরও safe হয়।

উদাহরণ:

```ts
interface User {
  name: string;
  age: number;
}

type Keys = keyof User; 
// "name" | "age"
```

# **Blog 3: any, unknown আর never – তিনটার সহজ পার্থক্য**

**any:**
সবচেয়ে risky টাইপ। কিছুই check করে না।
যে কোনো মান, যে কোনো operation allowed।

**unknown:**
এটা safer any.
Value রাখা যাবে, কিন্তু কিছু করতে চাইলে আগে type-check করতে হবে।

**never:**
এই টাইপ কখনো কোনো মান ধরে না।
যেমন কোনো function যেটা সবসময় error throw করে বা return করে না।


# **Blog 4: Enum কেন ব্যবহার করা হয়? (Numeric ও String Enum)**

Enum হলো কিছু নির্দিষ্ট constant মানকে সাজিয়ে রাখার একটি উপায়। এতে কোড পরিষ্কার থাকে।

**Numeric Enum:**

```ts
enum Direction {
  Up,
  Down,
  Left,
  Right
}
```

এগুলো auto-numbered হয় (0,1,2,3)।

**String Enum:**

```ts
enum Role {
  Admin = "ADMIN",
  User = "USER"
}
```


# **Blog 5: Union আর Intersection Type – সহজ ব্যাখ্যা**

**Union (`|`)**
মানে → Either this or that
একটি variable একাধিক type হতে পারে।

Example:

```ts
let id: string | number;
```

**Intersection (`&`)**
মানে → This and that
একটি value-এর ভিতরে দুইটাই থাকতে হবে।

Example:

```ts
interface A { name: string }
interface B { age: number }

type Person = A & B;
```