To connect a **NestJS** application to **MongoDB** using **Mongoose**, follow these steps:

### Step 1: Install Required Packages

In your NestJS project directory, install Mongoose and the NestJS Mongoose package:

```bash
npm install @nestjs/mongoose mongoose
```

### Step 2: Configure the Mongoose Connection in NestJS

1. Open your **app module** (typically `app.module.ts`).
2. Import `MongooseModule` from `@nestjs/mongoose`.
3. Use `MongooseModule.forRoot()` in the `imports` array to connect to MongoDB.

```typescript
// src/app.module.ts
import { Module } from '@nestjs/common';
import { MongooseModule } from '@nestjs/mongoose';
import { AppController } from './app.controller';
import { AppService } from './app.service';

@Module({
  imports: [
    MongooseModule.forRoot('mongodb://localhost:27017/mydatabase', {
      useNewUrlParser: true,
      useUnifiedTopology: true,
    }),
  ],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}
```

> Replace `'mongodb://localhost:27017/mydatabase'` with your MongoDB URI.

### Step 3: Define a Mongoose Schema

In NestJS, define your Mongoose schema by creating a model with a TypeScript interface and a schema decorator.

1. Create a new module (e.g., `cats` module) and add your schema.

   ```bash
   nest generate module cats
   nest generate service cats
   ```

2. Define the schema with a model and decorator in a new file (e.g., `cats.schema.ts`):

   ```typescript
   // src/cats/schemas/cat.schema.ts
   import { Prop, Schema, SchemaFactory } from '@nestjs/mongoose';
   import { Document } from 'mongoose';

   export type CatDocument = Cat & Document;

   @Schema()
   export class Cat {
     @Prop({ required: true })
     name: string;

     @Prop()
     age: number;

     @Prop()
     breed: string;
   }

   export const CatSchema = SchemaFactory.createForClass(Cat);
   ```

3. Register the schema in the module:

   ```typescript
   // src/cats/cats.module.ts
   import { Module } from '@nestjs/common';
   import { MongooseModule } from '@nestjs/mongoose';
   import { CatsService } from './cats.service';
   import { Cat, CatSchema } from './schemas/cat.schema';

   @Module({
     imports: [MongooseModule.forFeature([{ name: Cat.name, schema: CatSchema }])],
     providers: [CatsService],
     exports: [CatsService],
   })
   export class CatsModule {}
   ```

### Step 4: Use the Model in a Service

1. Inject the model using `@InjectModel()` in the service.
2. Interact with the model using Mongoose methods (e.g., `find`, `create`, `update`, `delete`).

   ```typescript
   // src/cats/cats.service.ts
   import { Injectable } from '@nestjs/common';
   import { InjectModel } from '@nestjs/mongoose';
   import { Model } from 'mongoose';
   import { Cat, CatDocument } from './schemas/cat.schema';

   @Injectable()
   export class CatsService {
     constructor(@InjectModel(Cat.name) private catModel: Model<CatDocument>) {}

     async create(createCatDto: any): Promise<Cat> {
       const createdCat = new this.catModel(createCatDto);
       return createdCat.save();
     }

     async findAll(): Promise<Cat[]> {
       return this.catModel.find().exec();
     }
   }
   ```

### Step 5: Use the Service in a Controller

1. Inject the service into the controller.
2. Create endpoints to interact with MongoDB.

   ```typescript
   // src/cats/cats.controller.ts
   import { Controller, Get, Post, Body } from '@nestjs/common';
   import { CatsService } from './cats.service';

   @Controller('cats')
   export class CatsController {
     constructor(private readonly catsService: CatsService) {}

     @Post()
     async create(@Body() createCatDto: any) {
       return this.catsService.create(createCatDto);
     }

     @Get()
     async findAll() {
       return this.catsService.findAll();
     }
   }
   ```

### Step 6: Test Your NestJS Application

Start the application and test the endpoints to confirm MongoDB is connected:

```bash
npm run start
```

By following these steps, you’ll have a working NestJS application connected to MongoDB via Mongoose, ready for CRUD operations and other MongoDB interactions.
