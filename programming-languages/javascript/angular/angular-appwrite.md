## Connect App to Appwrite backend

### 1. **Set Up Appwrite Backend**

#### **a. Install and Run Appwrite**

- Follow the instructions on the [Appwrite website](https://appwrite.io/docs/installation) to install and run Appwrite.
- You can set it up locally using Docker or deploy it to a server.

#### **b. Create a Project in Appwrite**

- Go to your Appwrite dashboard (`http://localhost` or your Appwrite domain).
- Create a new project by providing a name and a unique project ID.
- Note the project ID and API endpoint URL, as these will be used in your Angular app.

#### **c. Set Up API Keys (Optional)**

- Go to the Appwrite dashboard, select your project, and navigate to **API Keys**.
- Create an API key with permissions according to your needs. (For example, read, write access to database collections).
- This API key is useful if you're using server-to-server API calls in your app.

---

### 2. **Install Appwrite SDK in Angular Project**

In your Angular project, install the Appwrite SDK with npm:

```bash
npm install appwrite
```

### 3. **Configure Appwrite SDK in Angular**

Create a service in Angular to manage Appwrite interactions. This service will initialize the Appwrite client and handle requests to the Appwrite backend.

1. **Generate a Service**: Use Angular CLI to generate a service.

   ```bash
   ng generate service services/appwrite
   ```

2. **Set Up the Appwrite Client** in the generated `appwrite.service.ts` file:

   ```typescript
   import { Injectable } from '@angular/core';
   import { Client, Account, Databases } from 'appwrite';

   @Injectable({
     providedIn: 'root',
   })
   export class AppwriteService {
     private client: Client;
     private account: Account;
     private database: Databases;

     constructor() {
       this.client = new Client()
         .setEndpoint('http://localhost/v1') // Replace with your Appwrite endpoint
         .setProject('YOUR_PROJECT_ID'); // Replace with your project ID

       // Initialize services
       this.account = new Account(this.client);
       this.database = new Databases(this.client);
     }

     // Authentication methods
     async createAccount(email: string, password: string, name: string) {
       return this.account.create('unique()', email, password, name);
     }

     async login(email: string, password: string) {
       return this.account.createEmailSession(email, password);
     }

     async logout() {
       return this.account.deleteSession('current');
     }

     // Database CRUD operations
     async createDocument(collectionId: string, data: any) {
       return this.database.createDocument('YOUR_DATABASE_ID', collectionId, 'unique()', data);
     }

     async listDocuments(collectionId: string) {
       return this.database.listDocuments('YOUR_DATABASE_ID', collectionId);
     }

     async deleteDocument(collectionId: string, documentId: string) {
       return this.database.deleteDocument('YOUR_DATABASE_ID', collectionId, documentId);
     }
   }
   ```

Replace `YOUR_PROJECT_ID` and `YOUR_DATABASE_ID` with your actual Appwrite project and database IDs. The `AppwriteService` can now perform operations for authentication, database creation, and document CRUD operations.

---

### 4. **Using the Appwrite Service in Angular Components**

You can inject the `AppwriteService` into any component to perform backend operations.

For example, a login function in a component could look like this:

```typescript
import { Component } from '@angular/core';
import { AppwriteService } from './services/appwrite.service';

@Component({
  selector: 'app-login',
  templateUrl: './login.component.html',
})
export class LoginComponent {
  constructor(private appwriteService: AppwriteService) {}

  async login(email: string, password: string) {
    try {
      await this.appwriteService.login(email, password);
      console.log('Login successful!');
    } catch (error) {
      console.error('Login failed:', error);
    }
  }
}
```

### 5. **Testing and Debugging**

To ensure everything is working:

- Start your Angular application.
- Test functionalities like logging in, creating an account, or performing database operations.
- Monitor Appwrite’s console for any API requests and responses to debug issues.

---

### 6. **Optional: Deploy Appwrite and Angular**

If you're deploying Appwrite and Angular, ensure that:

- Appwrite is accessible from your Angular frontend (e.g., through an IP address or domain).
- Update `setEndpoint` in your Appwrite client configuration to reflect the correct production endpoint URL.
