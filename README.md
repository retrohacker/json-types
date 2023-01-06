# @retrohacker/json-types

Types to help dealing with unstructured JSON payloads.

## Types

```typescript
export type JsonPrimitive = string | number | boolean | null
export type JsonValue = JsonPrimitive | JsonObject | JsonArray
export type JsonObject = { [key: string]: JsonValue }
export type JsonArray = JsonValue[]
```

## Usage

```typescript
import { JsonObject } from 'json-types'

type User = {
  id: number,
  name: string,
  email: string
}
const { statusCode, body } = await request(
  `http://localhost:3000/user/42`
);

if (statusCode !== 200) {
  return null;
}

const remoteUser = (await body.json()) as JsonObject;
const localUser:User = {
  id: 42
};

localUser.name = [
  remoteUser.firstName,
  remoteUser.middleName,
  remoteUser.lastName,
]
  .filter((s) => s)
  .join(" ");

if (typeof remoteUser.emailAddress === "string") {
  localUser.email = remoteUser.emailAddress;
}
```
