# Auth And Status Codes

Authentication checks who the user is.

Authorization checks what the user can access.

Common auth types:

- Basic auth
- Bearer token
- API key
- OAuth token
- Session cookie

Important auth tests:

- No token
- Invalid token
- Expired token
- Token for wrong role
- Token reuse after logout
- Access another user's data

Status code habit:

- Check status code.
- Check response body.
- Check error message.
- Check headers.
- Check database or downstream impact.

