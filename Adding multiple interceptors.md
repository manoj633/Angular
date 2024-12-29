Register multiple HTTP interceptors by providing them in the `providers` array of your Angular module. Each interceptor is registered with the `HTTP_INTERCEPTORS` token using the `multi: true` option to indicate that multiple interceptors can be chained together.

Here's an example of how to set up an Angular module with two interceptors: one for logging requests and responses, and another for adding a specific header to all outgoing requests.

### Step 1: Create the Logging Interceptor

This interceptor will log all outgoing requests and incoming responses.

```typescript
import { Injectable } from '@angular/core';
import { HttpEvent, HttpInterceptor, HttpHandler, HttpRequest, HttpResponse } from '@angular/common/http';
import { Observable } from 'rxjs';
import { tap } from 'rxjs/operators';

@Injectable()
export class LoggingInterceptor implements HttpInterceptor {
  intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
    console.log('Outgoing request to:', req.url);
    return next.handle(req).pipe(
      tap(event => {
        if (event instanceof HttpResponse) {
          console.log('Incoming response from:', req.url);
        }
      })
    );
  }
}
```

### Step 2: Create Another Interceptor for Adding Headers

This interceptor adds a custom header to all outgoing requests.

```typescript
import { Injectable } from '@angular/core';
import { HttpEvent, HttpInterceptor, HttpHandler, HttpRequest } from '@angular/common/http';
import { Observable } from 'rxjs';

@Injectable()
export class HeaderInterceptor implements HttpInterceptor {
  intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>> {
    const modifiedRequest = req.clone({
      headers: req.headers.set('Custom-Header', 'Value')
    });
    return next.handle(modifiedRequest);
  }
}
```

### Step 3: Register Both Interceptors in the Angular Module

You need to add both interceptors to the `HTTP_INTERCEPTORS` array in your module’s providers.

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { HttpClientModule, HTTP_INTERCEPTORS } from '@angular/common/http';
import { AppComponent } from './app.component';
import { LoggingInterceptor } from './logging.interceptor';
import { HeaderInterceptor } from './header.interceptor';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    HttpClientModule
  ],
  providers: [
    {
      provide: HTTP_INTERCEPTORS,
      useClass: LoggingInterceptor,
      multi: true
    },
    {
      provide: HTTP_INTERCEPTORS,
      useClass: HeaderInterceptor,
      multi: true
    }
  ],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

### Explanation

- **Multiple Interceptors**: Both interceptors are provided with the `HTTP_INTERCEPTORS` token. The `multi: true` option allows Angular to chain these interceptors.
- **Order of Execution**: The order in which interceptors are provided is the order in which they will execute. In this example, the `LoggingInterceptor` will run before the `HeaderInterceptor`.

This setup ensures that every HTTP request first gets logged and then has a header added before it is sent out. Similarly, every response is logged after it is received.