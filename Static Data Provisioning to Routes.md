In Angular, you can provide static data to routes using the `data` property in the route configuration. This is useful for passing configuration information or static content that a component might need to render. Here's how you can set it up and access it in your components:

### Setting Up Static Data in Routes

When defining your routes, you can add a `data` property to each route. This property is an object where you can define key-value pairs of static data.

```typescript
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { HomeComponent } from './home/home.component';
import { AboutComponent } from './about/about.component';

const routes: Routes = [
  { path: 'home', component: HomeComponent },
  { 
    path: 'about', 
    component: AboutComponent,
    data: { title: 'About Us', description: 'This is the about page' }
  }
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

### Accessing Static Data in Components

To access the static data provided in the route, you can use Angular's `ActivatedRoute` service. This service provides access to the route's data through an observable.

Here's how you can access the static data in a component:

```typescript
import { Component, OnInit } from '@angular/core';
import { ActivatedRoute } from '@angular/router';

@Component({
  selector: 'app-about',
  template: `
    <h1>{{ title }}</h1>
    <p>{{ description }}</p>
  `
})
export class AboutComponent implements OnInit {
  title: string;
  description: string;

  constructor(private route: ActivatedRoute) {}

  ngOnInit() {
    this.route.data.subscribe(data => {
      this.title = data['title'];
      this.description = data['description'];
    });
  }
}
```

### Key Points

- **Data Property**: The `data` property in the route configuration is used to pass static data to the route. It is an object that can contain any key-value pairs.

- **ActivatedRoute**: Use the `ActivatedRoute` service to access the route's data. The `data` property of `ActivatedRoute` is an observable that you can subscribe to in order to get the static data.

- **Use Cases**: Static data is useful for passing configuration settings, titles, or any other static information that a component might need to render.

- **No Re-Rendering**: Since the data is static, it doesn't trigger re-rendering of the component unless the route changes.

By using static data provisioning, you can simplify the process of passing non-dynamic information to your components, making your application more organized and easier to maintain.
        