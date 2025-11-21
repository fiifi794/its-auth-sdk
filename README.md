# @its/auth-sdk

Auto-generated TypeScript Angular SDK for the ITS Authentication API.

## Installation

```bash
pnpm add @its/auth-sdk
```

or

```bash
npm install @its/auth-sdk
```

## Usage

### Basic Configuration

```typescript
import { AuthApi, Configuration } from '@its/auth-sdk';
import { HttpClient } from '@angular/common/http';

// Create configuration with your API base path and token provider
const configuration = new Configuration({
  basePath: 'http://localhost:8000',
  accessToken: 'your-access-token-here',
});

// Create API client
const authApi = new AuthApi(new HttpClient(/* ... */), '', configuration);

// Use the API
authApi.apiV1AuthLoginCreate({ username: 'user', password: 'pass' }).subscribe(
  (response) => console.log('Login successful:', response),
  (error) => console.error('Login failed:', error)
);
```

### With Angular Dependency Injection

```typescript
import { Injectable } from '@angular/core';
import { AuthApi, Configuration } from '@its/auth-sdk';
import { HttpClient } from '@angular/common/http';

@Injectable({
  providedIn: 'root',
})
export class AuthService {
  private authApi: AuthApi;

  constructor(private http: HttpClient) {
    const config = new Configuration({
      basePath: environment.apiUrl,
      accessToken: this.getAccessToken(),
    });
    this.authApi = new AuthApi(this.http, '', config);
  }

  login(credentials: any) {
    return this.authApi.apiV1AuthLoginCreate(credentials);
  }

  getAccessToken() {
    // Retrieve from AuthFacade or secure storage
    return sessionStorage.getItem('access_token') || '';
  }
}
```

## API Endpoints

The SDK includes generated clients for:

- **Authentication**: Login, logout, token refresh, token verification
- **User Management**: Get current user, update profile
- **Permissions**: Check user permissions and roles

## Versioning

This SDK is automatically generated from the OpenAPI spec in the `fiifi794/its-specs` repository. Version numbers follow semantic versioning and map to the API version defined in the spec.

## Development

The SDK is generated automatically via GitHub Actions whenever the OpenAPI specification changes. To regenerate locally:

```bash
pip install openapi-generator-cli

openapi-generator-cli generate \
  -g typescript-angular \
  -i https://raw.githubusercontent.com/fiifi794/its-specs/main/auth-mvc.yml \
  -o generated \
  --additional-properties=npmName="@its/auth-sdk",ngVersion="21"
```

## License

MIT
