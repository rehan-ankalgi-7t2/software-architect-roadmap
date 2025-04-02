### **🚀 Prisma Schema Modelling Cheatsheet 🚀**  
A quick reference for defining models, relationships, and constraints in Prisma.

---

## **🛠 Basic Model Structure**
```prisma
model ModelName {
  id        Int      @id @default(autoincrement())  // Primary Key
  createdAt DateTime @default(now())               // Timestamp
  updatedAt DateTime @updatedAt                    // Auto-update timestamp
}
```

---

## **🔗 Relationships in Prisma**

### **1️⃣ One-to-One Relationship**
```prisma
model User {
  id    Int     @id @default(autoincrement())
  email String  @unique
  profile Profile? @relation(fields: [profileId], references: [id])
  profileId Int?  // Foreign key (nullable)
}

model Profile {
  id     Int    @id @default(autoincrement())
  bio    String
  user   User?  @relation(fields: [userId], references: [id])
  userId Int?   // Foreign key (nullable)
}
```
✔️ Each **User** has **one Profile**, and each **Profile** belongs to **one User**.

---

### **2️⃣ One-to-Many Relationship**
```prisma
model User {
  id        Int         @id @default(autoincrement())
  email     String      @unique
  posts     Post[]
}

model Post {
  id      Int     @id @default(autoincrement())
  title   String
  user    User    @relation(fields: [userId], references: [id])
  userId  Int
}
```
✔️ **One User → Multiple Posts**, but **One Post → One User**.

---

### **3️⃣ Many-to-Many Relationship**
```prisma
model Student {
  id        Int       @id @default(autoincrement())
  name      String
  courses   Course[]  @relation("Enrollment")
}

model Course {
  id        Int       @id @default(autoincrement())
  title     String
  students  Student[] @relation("Enrollment")
}
```
✔️ A **Student** can enroll in **multiple Courses**, and a **Course** can have **multiple Students**.

---

## **🔒 Constraints & Indexing**

### **1️⃣ Unique Constraint**
```prisma
model User {
  id    Int    @id @default(autoincrement())
  email String @unique  // Ensures unique email
}
```

### **2️⃣ Composite Unique Constraint**
```prisma
model Post {
  id      Int    @id @default(autoincrement())
  title   String
  author  String
  @@unique([title, author])  // Unique combination of title & author
}
```

### **3️⃣ Indexing for Performance**
```prisma
model Product {
  id    Int    @id @default(autoincrement())
  name  String
  sku   String @unique
  @@index([name])  // Creates an index on "name"
}
```

---

## **⚡ Default Values & Data Types**

### **1️⃣ Default Values**
```prisma
model Order {
  id          Int      @id @default(autoincrement())
  status      String   @default("pending")
  createdAt   DateTime @default(now())
}
```

### **2️⃣ Enum Types**
```prisma
enum Role {
  USER
  ADMIN
  MODERATOR
}

model User {
  id   Int   @id @default(autoincrement())
  role Role  @default(USER)
}
```

---

## **🛠 Soft Deletes (Logical Deletion)**
```prisma
model User {
  id        Int      @id @default(autoincrement())
  email     String   @unique
  deletedAt DateTime?
}
```
✔️ Instead of deleting records, set `deletedAt` to `now()`.

---

## **🔗 Self-Referencing (Hierarchical Data)**
```prisma
model Employee {
  id        Int        @id @default(autoincrement())
  name      String
  managerId Int?       
  manager   Employee?  @relation(fields: [managerId], references: [id])
  subordinates Employee[] @relation("Manager")
}
```
✔️ **Employees** can have a **manager** and **subordinates**.

---

## **🚀 Prisma Migrations & Commands**
### **1️⃣ Initialize Prisma**
```sh
npx prisma init
```
### **2️⃣ Run Migrations**
```sh
npx prisma migrate dev --name init
```
### **3️⃣ Generate Prisma Client**
```sh
npx prisma generate
```
### **4️⃣ Seed Database**
```sh
npx prisma db seed
```
### **5️⃣ View Database**
```sh
npx prisma studio
```

---

## **📌 Quick Reference for Data Types**
| Type          | Description                         |
|--------------|------------------------------------|
| `String`     | Text data                          |
| `Int`        | Integer (auto-increment possible) |
| `Float`      | Decimal values                     |
| `Boolean`    | `true` or `false`                  |
| `DateTime`   | Timestamp                          |
| `Json`       | Stores JSON objects                |
| `Bytes`      | Binary data (files, images, etc.) |

---

## **🔥 Summary**
- ✅ **Use `@relation()` for defining relationships.**
- ✅ **`@unique` & `@@index()` help optimize queries.**
- ✅ **Use Enums (`enum Role {}`) for predefined values.**
- ✅ **Apply Soft Deletes with `deletedAt DateTime?`.**
- ✅ **Run `npx prisma migrate dev` to update the database.**

---

🚀 **Want a deep dive into Prisma?** Let me know! 😊
