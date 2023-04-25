# QR scanner app for events

## API

### 1. App scans connection QR code. The code contains only an URL.

The app makes a POST request to the URL:

POST {url}

```ts
interface ConnectData {
  id: string;
  model: string;
  systemName: string;
  systemVersion: string;
}
```

### 2. Server must respond with the following data format:

HTTP 200

```ts
interface ConnectSuccessResponse {
  token: string;
  url: string;
  header?: string;
  message?: string[];
}
```

HTTP 403

```ts
interface ConnectFailedResponse {
  error: string;
  info?: string[];
}
```

### 3. App enters scan mode mode. For each scanned QR code app makes a POST request to the URL from step 2 with token from step 2:

POST {url}
Authorization: Token {token}

```ts
interface ScanData {
  code: string;
  serviceId?: number;
}
```

### 4. Server must respond in the following format:

HTTP 200

```ts
interface ScanSuccessResponse {
  success: boolean;
  header: string;
  message?: string[];
  color?: string;
  backgroundColor?: string;
  services?: {
    name: string;
    id: number;
    redeemed: boolean;
  }[];
}
```
