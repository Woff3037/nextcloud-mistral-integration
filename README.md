# Nextcloud-Mistral AI Integration

A Nextcloud app that acts as a secure backend bridge between **Nextcloud** and **Mistral AI**, enabling Mistral AI to access calendar, files, emails, and contacts via Nextcloud APIs.

---

## **Features**
- **Secure API Access**: OAuth2/App Password authentication for Nextcloud.
- **Data Endpoints**: Calendar (CalDAV), Files (WebDAV), Emails (IMAP), Contacts (CardDAV).
- **Minimal UI**: No frontend in Nextcloud; all interactions via API.
- **Granular Permissions**: Control what Mistral AI can read/write.
- **Audit Logging**: Track all API requests and responses.

---

## **Prerequisites**
- Nextcloud server (v27+ recommended)
- PHP 8.1+
- Mistral AI API access (API key or custom tool integration)

---

## **Installation**
1. Clone this repository into your Nextcloud `apps` directory:
  ```bash
  git clone https://github.com/your-username/nextcloud-mistral-integration.git
  ```

2. Enable the app in Nextcloud:
  ```bash
  php occ app:enable mistral_integration
  ```
```
  ```
3. Configure the app via Nextcloud’s admin settings or `config.php`.

---

## **Configuration**

### **Nextcloud Side**

- Generate an **App Password** or set up **OAuth2** for Nextcloud API access.
- Ensure the app has permissions for:
  - Calendar (CalDAV)
  - Files (WebDAV)
  - Emails (IMAP)
  - Contacts (CardDAV)

### **Mistral AI Side**

- Add your Nextcloud server’s API endpoint to Mistral AI’s allowed sources.
- Use the provided API key or token for authentication.

---

## **API Endpoints**


| Endpoint        | Method | Description                                                     |
| --------------- | ------ | --------------------------------------------------------------- |
| `/api/calendar` | GET    | Fetch calendar events (supports `start` and `end` query params) |
| `/api/files`    | GET    | List files in a directory (supports `path` query param)         |
| `/api/emails`   | GET    | Fetch emails (supports `limit` and `offset` query params)       |
| `/api/contacts` | GET    | Fetch contacts                                                  |


**Authentication**: All endpoints require a `Bearer` token in the `Authorization` header.

---

## **Example Usage**

### Fetch Calendar Events

```bash
curl -X GET "http://your-nextcloud-server.com/apps/mistral_integration/api/calendar?start=2026-06-28&end=2026-06-29" \
     -H "Authorization: Bearer YOUR_MISTRAL_API_KEY"
```

### List Files

```bash
curl -X GET "http://your-nextcloud-server.com/apps/mistral_integration/api/files?path=/Documents" \
     -H "Authorization: Bearer YOUR_MISTRAL_API_KEY"
```

---

## **Security**

- All data is transmitted over **HTTPS**. 
- Credentials are stored encrypted in Nextcloud’s database.
- Rate limiting and IP whitelisting are recommended.

---

## **Contributing**

1. Fork the repository.
2. Create a feature branch (`git checkout -b feature/your-feature`).
3. Commit your changes (`git commit -am 'Add new feature'`).
4. Push to the branch (`git push origin feature/your-feature`).
5. Open a Pull Request.
