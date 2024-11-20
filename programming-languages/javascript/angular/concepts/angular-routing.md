Routing in Angular enables navigation between different views or components within a single-page application (SPA). Angular provides the **Angular Router** module, which handles routing, navigation, and URL manipulation.

Here’s an overview of Angular routing:

---

### 1. **Setting Up Routing in Angular**

#### Install the Angular Router
The router is included by default when creating a new Angular application using the Angular CLI. If it isn't already added, you can install it:

```bash
ng add @angular/router
```

#### Add a `RouterModule` to Your Application
You need to configure routes in the app’s routing module:

```bash
ng generate module app-routing --flat --module=app
```

This generates an `app-routing.module.ts` file, where you define and manage application routes.

---

### 2. **Defining Routes**

A route is an object with two main properties:
- **path**: URL segment.
- **component**: The component associated with the route.

Example of route configuration:

```typescript
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { HomeComponent } from './home/home.component';
import { AboutComponent } from './about/about.component';

const routes: Routes = [
  { path: '', redirectTo: '/home', pathMatch: 'full' }, // Default route
  { path: 'home', component: HomeComponent },
  { path: 'about', component: AboutComponent },
  { path: '**', redirectTo: '/home' } // Wildcard route for invalid paths
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule {}
```

---

### 3. **Using the Router Outlet**

The `<router-outlet>` directive acts as a placeholder to render components based on the current route.

In `app.component.html`:

```html
<nav>
  <a routerLink="/home">Home</a>
  <a routerLink="/about">About</a>
</nav>
<router-outlet></router-outlet>
```

---

### 4. **RouterLink Directive**

Use the `routerLink` directive to define navigation links. Example:

```html
<a routerLink="/home" routerLinkActive="active">Home</a>
```

- `routerLinkActive`: Adds a class when the link is active.

---

### 5. **Route Parameters**

You can pass parameters through routes.

#### Define a Route with Parameters
```typescript
{ path: 'profile/:id', component: ProfileComponent }
```

#### Access Parameters in the Component
Use Angular's `ActivatedRoute` service to access route parameters.

```typescript
import { ActivatedRoute } from '@angular/router';

constructor(private route: ActivatedRoute) {}

ngOnInit() {
  const id = this.route.snapshot.paramMap.get('id'); // Access parameter
}
```

---

### 6. **Child Routes**

Define nested routes for hierarchical navigation.

```typescript
const routes: Routes = [
  {
    path: 'dashboard',
    component: DashboardComponent,
    children: [
      { path: 'stats', component: StatsComponent },
      { path: 'settings', component: SettingsComponent }
    ]
  }
];
```

Render nested views using `<router-outlet>` inside the parent component’s template.

---

### 7. **Lazy Loading Modules**

Load feature modules lazily for better performance.

#### Configure Lazy Loading
```typescript
const routes: Routes = [
  {
    path: 'features',
    loadChildren: () => import('./features/features.module').then(m => m.FeaturesModule)
  }
];
```

#### Create a Feature Module
```bash
ng generate module features --route features --module app
```

---

### 8. **Guards**

Guards control access to routes. Common guards include:
- **CanActivate**: Checks if a route can be activated.
- **CanDeactivate**: Checks if a route can be exited.
- **Resolve**: Preloads data before navigation.

#### Example of a `CanActivate` Guard
```typescript
import { Injectable } from '@angular/core';
import { CanActivate, Router } from '@angular/router';

@Injectable({
  providedIn: 'root',
})
export class AuthGuard implements CanActivate {
  constructor(private router: Router) {}

  canActivate(): boolean {
    const isLoggedIn = !!localStorage.getItem('token');
    if (!isLoggedIn) {
      this.router.navigate(['/login']);
    }
    return isLoggedIn;
  }
}
```

---

### 9. **Query Parameters**

Pass and retrieve query parameters.

#### Navigate with Query Params
```html
<a [routerLink]="['/search']" [queryParams]="{ query: 'Angular' }">Search</a>
```

#### Retrieve Query Params
```typescript
import { ActivatedRoute } from '@angular/router';

constructor(private route: ActivatedRoute) {}

ngOnInit() {
  this.route.queryParams.subscribe(params => {
    console.log(params['query']);
  });
}
```

---

### 10. **Navigation Programmatically**

Use the `Router` service to navigate programmatically.

```typescript
import { Router } from '@angular/router';

constructor(private router: Router) {}

navigateToAbout() {
  this.router.navigate(['/about']);
}
```

---

Angular’s routing system is flexible and powerful, offering features such as guards, lazy loading, route resolvers, and more to create robust SPAs. Let me know if you'd like to dive deeper into any specific aspect!
