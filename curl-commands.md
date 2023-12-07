# Curl Commands

Export the Bearer token to be used for the Authorization header

- This can be retrieved by inspecting the web page of your running instance of Backstage and looking through the different network calls for the Authorization header

```bash
export token='...token...'
```

Create a role in the RBAC Backend plugin, this is assuming that your Backstage instance is running locally with the `backend.baseUrl` set to <http://localhost:7007>.

```bash
curl -X POST "http://localhost:7007/api/permission/roles" -d '{ "memberReferences":  [ "user:default/pataknight" ], "name": "role:default/curl-test" }' -H "Content-Type: application/json" -H "Authorization: Bearer $token" -v
```

Assign a permission to a role

```bash
curl -X POST "http://localhost:7007/api/permission/policies" -d '{"entityReference":"role:default/curl-test", "permission": "catalog.location.create", "policy": "create", "effect":"allow"}' -H "Content-Type: application/json" -H "Authorization: Bearer $token" -v
```

Get all roles

```bash
curl -X GET "http://localhost:7007/api/permission/roles" -H "Content-Type: application/json" -H "Authorization: Bearer $token" -v
```

Get all permission policies

```bash
curl -X GET "http://localhost:7007/api/permission/policies" -H "Content-Type: application/json" -H "Authorization: Bearer $token" -v
```
