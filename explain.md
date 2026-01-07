# WEEK05 LAB5-JAVASCRIPT-Fundamentals

## 01-variables.js

### Challenge: Create a Person Object

```text
- === Challenge: Person Object ===
  Student object:
  {
  firstName: 'Alice',
  lastName: 'Smith',
  age: 20,
  gpa: 3.8,
  courses: [ 'HTML', 'CSS', 'JavaScript' ],
  isActive: true,
  getFullName: [Function: getFullName],
  getInfo: [Function: getInfo]
  }
```

### 1. ความหมายของ Student Object

Student Object เป็น Object ในภาษา JavaScript ที่ใช้เก็บข้อมูลของนักเรียน 1 คน  
ภายใน Object จะประกอบด้วย

- **Properties** (ข้อมูล)
- **Methods** (ฟังก์ชันที่ทำงานกับข้อมูลภายใน Object)

### 2. Properties (คุณสมบัติของ Object)

- **firstName**

เก็บชื่อจริงของนักเรียน

ชนิดข้อมูล: String

- **lastName**

เก็บนามสกุลของนักเรียน

ชนิดข้อมูล: String

- **age**

เก็บอายุของนักเรียน

ชนิดข้อมูล: Number

- **gpa**

เก็บเกรดเฉลี่ย

ชนิดข้อมูล: Number

- **courses**

เก็บรายชื่อวิชาที่นักเรียนลงเรียน
ชนิดข้อมูล: Array
สามารถเข้าถึงข้อมูลได้ด้วย index เช่น
courses[0] → HTML

- **isActive**

แสดงสถานะของนักเรียน

ชนิดข้อมูล: Boolean

ค่า true หมายถึงยังเป็นนักเรียนอยู่

### 3. Methods (ฟังก์ชันภายใน Object)

```text
student.getFullName();
```

- **การทำงาน**
- this หมายถึง object student
- ดึงค่า this.firstName
- ดึงค่า this.lastName
- นำค่าทั้งสองมาต่อกันเป็นชื่อเต็ม

```text
student.getInfo();
```

- เรียกใช้ this.getFullName() เพื่อดึงชื่อนามสกุล และดึงค่า this.age และ this.gpa เพื่อรวมข้อมูลเป็นข้อความเดียว

```text
Name: Alice Smith, Age: 20, GPA: 3.8
```

### 4. หลักการทำงานของ this

- this คือการอ้างอิงถึง object ปัจจุบัน ทำให้ method สามารถเข้าถึง property ภายใน object เดียวกันได้

## 02-functions.js

### 8. Returning Objects

```text
function createUser(firstName, lastName, age) {
  return {
    firstName, // shorthand for firstName: firstName  --  สําคัญมาก
    lastName,
    age,
    email: `${firstName.toLowerCase()}.${lastName.toLowerCase()}@example.com`,
    getFullName() {
      // shorthand for getFullName: function() {}
      return `${this.firstName} ${this.lastName}`;
    },
    getAge() {
      return this.age;
    },
  };
}

console.log("\nReturning Objects:");
const newUser = createUser("John", "Doe", 30);
console.log(newUser);
console.log("Email:", newUser.email);
console.log("Full name:", newUser.getFullName());
```

ฟังก์ชัน `createUser` ใช้สำหรับสร้างและส่งกลับ (return) Object ของผู้ใช้ 1 คน

- **การทำงานโดยย่อ**

1. ฟังก์ชันรับค่า `firstName`, `lastName`, และ `age`
2. สร้าง Object ใหม่จากค่าที่รับมา โดยใช้ **property shorthand**
3. สร้าง `email` อัตโนมัติจากชื่อและนามสกุล
4. มี method สำหรับ
   - `getFullName()` → คืนค่าชื่อ-นามสกุล
   - `getAge()` → คืนค่าอายุ
5. เมื่อเรียกฟังก์ชัน จะได้ Object ใหม่เก็บไว้ในตัวแปร

## ตัวอย่างการใช้งาน

```js
const newUser = createUser("John", "Doe", 30);
```

### 9. Function as Parameter (Callback)

```js
function processArray(arr, callback) {
  const result = [];
  for (const item of arr) {
    result.push(callback(item));
  }
  return result;
}

const numbers = [1, 2, 3, 4, 5];
const doubled = processArray(numbers, (x) => x * 2);
const squared = processArray(numbers, (x) => x * x);

console.log("\nCallback Function:");
console.log("Original:", numbers);
console.log("Doubled:", doubled);
console.log("Squared:", squared);
```

ฟังก์ชัน `processArray` ใช้ **Callback** เพื่อประมวลผลแต่ละค่าใน Array และคืนค่า Array ใหม่

**การทำงานโดยสั้น ๆ:**

1. รับ Array และ Callback Function
2. วนแต่ละค่าใน Array
3. ส่งค่าไปให้ Callback แล้วเก็บผลลัพธ์
4. คืนค่า Array ใหม่

**ตัวอย่าง:**

```js
const numbers = [1, 2, 3, 4, 5];
const doubled = processArray(numbers, (x) => x * 2); // [2,4,6,8,10]
const squared = processArray(numbers, (x) => x * x); // [1,4,9,16,25]
```

## 03-control-flow.js

### 5. Short-Circuit Evaluation

```js
console.log("\nShort-Circuit Evaluation:");

const user = { name: "John", age: 25 };
const admin = null;

// OR: use default value
const userName = admin?.name || user.name || "Anonymous";
console.log("User name:", userName);
// ?. คือการใช้ Optional Chaining - เป็นวิธีที่ปลอดภัยในการเข้าถึง properties ของ object ที่อาจเป็น null หรือ undefined
// admin?.name ก็คือ ถ้า admin มีค่า ให้เข้าถึง .name ไม่เช่นนั ้นให้คืนค่า undefined
// 1. admin?.name
//   - admin คือ null ❌
//   - ไม่ error, ส่งคืน undefined
// 2. undefined || user.name
//   - user.name คือ "John" ✅
//   - ใช้ค่านี้ → "John"
// 3. ผลลัพธ์: "John"

// AND: check before accessing
const userProfile = user && user.profile;
console.log("User profile:", userProfile); // undefined
```

**แนวคิดหลัก:**

- `||` (OR) → คืนค่าตัวแรกที่เป็น truthy
- `&&` (AND) → คืนค่าตัวแรกที่เป็น falsy หรือค่าสุดท้ายถ้า truthy
- `?.` (Optional Chaining) → ปลอดภัยต่อ null / undefined

**ตัวอย่างในโค้ด:**

```js
const user = { name: "John", age: 25 };
const admin = null;

// OR: ใช้ค่า default
const userName = admin?.name || user.name || "Anonymous";
// admin?.name = undefined → user.name = "John" → userName = "John"

// AND: ตรวจสอบก่อนเข้าถึง property
const userProfile = user && user.profile;
// user.profile ไม่มี → undefined
```

**ผลลัพธ์:**

```text
User name: John
User profile: undefined
```

### 7. Form Validation

```js
function validateRegistration(formData) {
  // Create validation result object
  const errors = [];

  // Validate name
  if (!formData.name || formData.name.trim() === "") {
    errors.push("Name is required");
  } else if (formData.name.length < 3) {
    errors.push("Name must be at least 3 characters");
  }

  // Validate email
  if (!formData.email || formData.email.indexOf("@") === -1) {
    errors.push("Valid email is required");
  }

  // Validate age
  if (!formData.age || formData.age < 18) {
    errors.push("Must be 18 or older");
  }

  // Validate password
  if (!formData.password || formData.password.length < 6) {
    errors.push("Password must be at least 6 characters");
  }

  // Check if agree to terms
  if (!formData.agreeToTerms) {
    errors.push("Must agree to terms");
  }

  return {
    isValid: errors.length === 0,
    errors: errors,
  };
}

console.log("\nForm Validation:");

const validUser = {
  name: "John Doe",
  email: "john@example.com",
  age: 25,
  password: "securepass123",
  agreeToTerms: true,
};

const invalidUser = {
  name: "Jo",
  email: "invalidemail",
  age: 15,
  password: "pass",
  agreeToTerms: false,
};

console.log("Valid user:", validateRegistration(validUser));
console.log("Invalid user:", validateRegistration(invalidUser));
```

**แนวคิดหลัก:**

- ฟังก์ชัน `validateRegistration(formData)` ตรวจสอบข้อมูลผู้ใช้
- เก็บข้อผิดพลาดไว้ใน `errors` array
- คืนค่า Object:
  - `isValid` → true ถ้าไม่มี error
  - `errors` → รายการข้อผิดพลาด

**ตรวจสอบข้อมูล:**

1. Name → ต้องไม่ว่างและมี 3 ตัวอักษรขึ้นไป
2. Email → ต้องมี `@`
3. Age → ต้อง 18 ปีขึ้นไป
4. Password → ต้องมี 6 ตัวอักษรขึ้นไป
5. Agree to terms → ต้องเลือกยอมรับ

**ตัวอย่างผลลัพธ์:**

```js
validateRegistration(validUser);
// { isValid: true, errors: [] }

validateRegistration(invalidUser);
// { isValid: false, errors: [
//   "Name must be at least 3 characters",
//   "Valid email is required",
//   "Must be 18 or older",
//   "Password must be at least 6 characters",
//   "Must agree to terms"
// ]}
```

## 04-loops.js

### 9. Chaining methods

```js
console.log("\nMethod chaining:");
const data = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
// Filter even > map to string > join
const evenStrings = data
  .filter((n) => n % 2 === 0)
  .map((n) => `${n}²=${n * n}`)
  .join(", "); // "2²=4, 4²=16, ..."
// [2, 4, 6, 8, 10]
// ["2²=4", "4²=16", ...]
console.log("Even numbers squared:", evenStrings);
// Calculate average with reduce and length
const numbers2 = [10, 20, 30, 40, 50];
const average = numbers2.reduce((sum, n) => sum + n, 0) / numbers2.length;
console.log("Average:", average);
```

**แนวคิดหลัก:**

- **Method chaining** → เรียกหลาย method ต่อกันได้ เช่น `filter().map().join()`
- **Reduce** → ใช้ประมวลผล array เป็นค่าเดียว เช่น หาผลรวม

**Method Chaining**: เรียกหลาย method ต่อกัน เช่น `filter().map().join()`

- filter → เลือก element ตามเงื่อนไข
- map → แปลงค่า element
- join → รวมเป็น string

### 10. Challenge: Student Grades

```js
const students = [
  { name: "Alice", score: 95 },
  { name: "Bob", score: 75 },
  { name: "Charlie", score: 85 },
  { name: "Diana", score: 92 },
  { name: "Eve", score: 88 },
];
console.log("\nChallenge: Student Analysis");
console.log("Students:", students);
// 1. Get all names
const names = students.map((s) => s.name);
console.log("Names:", names.join(", "));
// 2. Filter high scorers (>= 85)
const highScorers = students.filter((s) => s.score >= 85);
console.log(
  "High scorers:",
  highScorers.map((s) => `${s.name} (${s.score})`).join(", ")
);
// 3. Calculate class average
const classAverage =
  students.reduce((sum, s) => sum + s.score, 0) / students.length;
console.log("Class average:", classAverage.toFixed(2));

// 4. Find top scorer
const topScorer = students.reduce((top, s) => (s.score > top.score ? s : top));
console.log("Top scorer:", `${topScorer.name} (${topScorer.score})`);

// 5. Create summary
const summary = students
  .map((s) => ({
    ...s,
    grade: s.score >= 90 ? "A" : s.score >= 80 ? "B" : "C",
  }))
  .sort((a, b) => b.score - a.score);
console.log("Summary (sorted):");
summary.forEach((s) => console.log(`  ${s.name}: ${s.score} (${s.grade})`));
```

ฟังก์ชันและแนวคิดที่ใช้ในการวิเคราะห์ข้อมูลนักเรียน:

1. **Get all names**

   - ใช้ `map` ดึงชื่อทุกคนจาก Array
   - ตัวอย่าง: `["Alice", "Bob", "Charlie", "Diana", "Eve"]`

2. **Filter high scorers**

   - ใช้ `filter` เลือกนักเรียนที่คะแนน >= 85
   - สามารถรวมชื่อและคะแนนด้วย `map` และ `join`

3. **Calculate class average**

   - ใช้ `reduce` รวมคะแนนทั้งหมด แล้วหารด้วยจำนวนคน
   - ผลลัพธ์เป็นค่าเฉลี่ยของชั้นเรียน

4. **Find top scorer**

   - ใช้ `reduce` เปรียบเทียบคะแนนทีละคน เพื่อหาคะแนนสูงสุด

5. **Create summary with grades**
   - ใช้ `map` เพิ่ม property `grade` ตามคะแนน
     - > = 90 → A, >= 80 → B, < 80 → C
   - ใช้ `sort` เรียงตามคะแนนจากสูงไปต่ำ
   - สามารถใช้ `forEach` แสดงสรุปรายชื่อพร้อมคะแนนและเกรด

**แนวคิดสำคัญ:**

- `map` → แปลงข้อมูล
- `filter` → เลือกข้อมูลตามเงื่อนไข
- `reduce` → รวมค่าหรือหาค่าสูงสุด/ต่ำสุด
- `sort` → จัดลำดับข้อมูล
- การสร้าง summary → ผสมหลายขั้นตอนเพื่อให้ได้ผลลัพธ์ครบใน Array เดียว

## 05-integration.js

### Activity 5: Integration - Quiz Application

```js
// Quiz data
const quizzes = [
  {
    question: "What is 5 + 3?",
    options: ["8", "7", "6", "9"],
    correctAnswer: 0, // Index of correct option
  },
  {
    question: "What is the capital of Thailand?",
    options: ["Phuket", "Bangkok", "Chiang Mai", "Pattaya"],
    correctAnswer: 1,
  },
  {
    question: "What is the largest planet?",
    options: ["Mars", "Saturn", "Jupiter", "Neptune"],
    correctAnswer: 2,
  },
  {
    quesion: "What is 2^8?",
    options: ["128", "256", "64", "512"],
    correctAnswer: 1,
  },
  {
    question: "Which is NOT a JavaScript data type?",
    options: ["string", "class", "symbol", "boolean"],
    correctAnswer: 1,
  },
];
// Quiz results
let results = [];
// Process each quiz
quizzes.forEach((quiz, index) => {
  const userAnswer = Math.floor(Math.random() * 4);
  const isCorrect = userAnswer === quiz.correctAnswer;
  results.push({
    questionNum: index + 1,
    question: quiz.question,
    userAnswer: quiz.options[userAnswer],
    correctAnswer: quiz.options[quiz.correctAnswer],
    isCorrect: isCorrect,
  });
});
// Display results
console.log("QUIZ RESULTS:");
console.log("─".repeat(60));
results.forEach((result) => {
  const status = result.isCorrect ? "✅ CORRECT" : "❌ WRONG";
  console.log(`Q${result.questionNum}: ${result.question}`);
  console.log(`  Your answer: ${result.userAnswer}`);
  if (!result.isCorrect) {
    console.log(`  Correct answer: ${result.correctAnswer}`);
  }
  console.log(`  ${status}`);
  console.log();
});
// Calculate score
const correctCount = results.filter((r) => r.isCorrect).length;
const score = (correctCount / results.length) * 100;
console.log("─".repeat(60));
console.log(
  `FINAL SCORE: ${correctCount}/${results.length} (${score.toFixed(1)}%)`
);
// จําลองการทํา quiz
// Grade assignment
let grade;
if (score >= 90) {
  grade = "A";
} else if (score >= 80) {
  grade = "B";
} else if (score >= 70) {
  grade = "C";
} else if (score >= 60) {
  grade = "D";
} else {
  grade = "F";
}
console.log(`GRADE: ${grade}`);
// Feedback
console.log("\nFEEDBACK:");
if (score === 100) {
  console.log("🌟🌟 Perfect score! Excellent work!");
} else if (score >= 80) {
  console.log("👍👍 Great job! Keep practicing.");
} else if (score >= 60) {
  console.log("📚📚 Good effort. Review the material and try again.");
} else {
  console.log("💪💪 Keep practicing. You'll improve!");
}
// Statistics
console.log("\n📊📊 STATISTICS:");
console.log(`Total questions: ${results.length}`);
console.log(`Correct: ${correctCount}`);
console.log(`Incorrect: ${results.length - correctCount}`);
console.log(`Success rate: ${score.toFixed(1)}%`);
// Category breakdown (if applicable)
const byCorrectness = results.reduce(
  (acc, r) => {
    acc[r.isCorrect ? "correct" : "incorrect"]++;
    return acc;
  },
  { correct: 0, incorrect: 0 }
);
console.log("\nAnswer breakdown:");
console.log(`  ✅ Correct: ${byCorrectness.correct}`);
console.log(`  ❌ Incorrect: ${byCorrectness.incorrect}`);
console.log("\n✅ All activities completed!");
console.log("━".repeat(60));
```

Quiz นี้เก็บคำถามใน array ของ object แต่ละข้อมีคำถาม ตัวเลือก และคำตอบที่ถูกต้อง

## การทำงานหลัก

1. **ตอบคำถามแบบสุ่ม**

   - วน `quizzes` ด้วย `forEach`
   - เลือกคำตอบของผู้ใช้แบบสุ่ม
   - เก็บผลลัพธ์ลง `results` (รวมสถานะถูก/ผิด)

2. **แสดงผล**

   - แสดงคำถาม
   - แสดงคำตอบผู้ใช้
   - ถ้าผิดจะแสดงคำตอบที่ถูกต้อง
   - แสดงสถานะถูก/ผิด

3. **คำนวณคะแนน & เกรด**

   - ใช้ `filter` หาจำนวนคำตอบถูก
   - คำนวณ % คะแนน
   - กำหนดเกรดตามช่วงคะแนน (A, B, C, D, F)
   - แสดงข้อความ feedback ตามเกรด

4. **สถิติ**
   - แสดงจำนวนคำถาม ทั้งหมด
   - แสดงจำนวนถูก และจำนวนผิด
   - แสดงอัตราความสำเร็จเป็น %
   - ใช้ `reduce` สรุปจำนวนถูก/ผิด

## แนวคิดสำคัญ

- loop array
- filter, reduce
- conditional logic
- template literal
