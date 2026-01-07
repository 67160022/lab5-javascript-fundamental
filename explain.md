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
