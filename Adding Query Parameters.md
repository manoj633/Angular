Adding query parameters to GET requests in an Angular application using the `HttpClient` module allows you to refine the data returned from a server. This is particularly useful for filtering, sorting, or specifying which fields to include in the response. Here’s a detailed guide on how to modify GET requests to include query parameters using the `HttpParams` class.

### 1. Understanding Query Parameters

Query parameters are key-value pairs that are appended to the URL of a GET request. They are typically used to pass information to the server to modify the response. For example, you might use query parameters to sort data, filter results, or specify pagination settings.

### 2. Using HttpParams to Append Query Parameters

The `HttpParams` class in Angular's `HttpClient` module provides a way to construct query parameters programmatically. Here’s how you can use it:

```typescript
import { Injectable } from '@angular/core';
import { HttpClient, HttpParams } from '@angular/common/http';
import { Observable } from 'rxjs';

@Injectable({
  providedIn: 'root'
})
export class DataService {

  constructor(private http: HttpClient) { }

  getDataWithParams(url: string, params: {[param: string]: string | number}): Observable<any> {
    let httpParams = new HttpParams();
    for (const key in params) {
      if (params.hasOwnProperty(key)) {
        httpParams = httpParams.set(key, params[key].toString());
      }
    }
    return this.http.get(url, { params: httpParams });
  }
}
```

In this service, the `getDataWithParams` method takes a URL and a parameters object as arguments. It constructs an `HttpParams` object by iterating over the parameters object and using the `set` method to append each key-value pair to the query string.

### 3. Use the Service in a Component

Inject the service into a component to use the `getDataWithParams` method. Pass the necessary query parameters when calling the method.

```typescript
import { Component, OnInit } from '@angular/core';
import { DataService } from './data.service';

@Component({
  selector: 'app-root',
  template: `<h1>Data from API with Parameters</h1>
             <div *ngFor="let item of data">
               {{ item | json }}
             </div>`
})
export class AppComponent implements OnInit {
  data: any;

  constructor(private dataService: DataService) {}

  ngOnInit() {
    const params = { sort: 'name', order: 'asc', limit: 10 };
    this.dataService.getDataWithParams('https://api.example.com/data', params)
      .subscribe(
        data => {
          this.data = data;
        },
        error => {
          console.error('There was an error!', error);
        }
      );
  }
}
```

### 4. Conclusion

Using `HttpParams` to append query parameters to GET requests in Angular allows for dynamic and flexible API calls. This method is essential for interacting with APIs that support various options for customizing responses based on parameters. Properly handling these parameters can significantly enhance the functionality of your application by allowing users to interact with data more effectively.