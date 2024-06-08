
# FastAPI with OAuth2 Proxy and NGINX

This project sets up a FastAPI application secured with OAuth2 Proxy and served by NGINX using Docker Compose. The OAuth2 Proxy is configured to use Google as the OAuth provider.

## Prerequisites

Before you start, ensure you have the following installed on your system:

- [Docker](https://www.docker.com/get-started)
- [Docker Compose](https://docs.docker.com/compose/install/)

## Project Structure

```
your-project-directory/
│
├── app/
│   └── main.py
├── Dockerfile.fastapi
├── Dockerfile.oauth2_proxy
├── Dockerfile.nginx
├── oauth2_proxy.cfg
├── nginx.conf
├── .env
└── docker-compose.yml
```

## Configuration

### Google OAuth2 Setup

1. **Create a new project**: [Google Cloud Console](https://console.developers.google.com/project).
2. **Choose the new project** from the top right project dropdown (only if another project is selected).
3. In the project Dashboard center pane, choose **"APIs & Services"**.
4. In the left Nav pane, choose **"Credentials"**.
5. In the center pane, choose the **"OAuth consent screen"** tab. Fill in "Product name shown to users" and hit save.
6. In the center pane, choose the **"Credentials"** tab.
7. Open the **"New credentials"** drop down.
8. Choose **"OAuth client ID"**.
9. Choose **"Web application"**.
10. Application name is freeform, choose something appropriate.
11. Authorized JavaScript origins is your domain, e.g., `http://localhost`.
12. Authorized redirect URIs is the location of `oauth2/callback`, e.g., `http://localhost/oauth2/callback`.
13. Choose **"Create"**.
14. Take note of the **Client ID** and **Client Secret**.
15. **Enable Admin SDK API**:
    - Under "APIs & Services", choose "Library".
    - Search for "Admin SDK" and enable it.
16. **Set up domain-wide delegation** (optional for restricting to specific Google groups):
    - Follow the steps [here](https://developers.google.com/workspace/guides/create-credentials#optional_set_up_domain-wide_delegation_for_a_service_account).

### Environment Variables

Create a `.env` file in the root of your project directory:

```ini
# .env
OAUTH2_PROXY_CLIENT_ID=your_google_client_id
OAUTH2_PROXY_CLIENT_SECRET=your_google_client_secret
OAUTH2_PROXY_COOKIE_SECRET=a_very_secure_32_byte_base64_secret
```

### Generate a Secure Cookie Secret

Generate a secure cookie secret using the following command:

```bash
openssl rand -base64 32
```

### Build and Run the Docker Containers

#### Build the Docker Images

```bash
docker-compose build
```

#### Start the Docker Containers

```bash
docker-compose up
```

### Access the Application

Open your web browser and navigate to [http://localhost](http://localhost). You should be redirected to the Google login page. After authenticating with your Google account, you will be redirected back to the FastAPI application.

## License

This project is licensed under the MIT License.

## Acknowledgments

- [FastAPI](https://fastapi.tiangolo.com/)
- [OAuth2 Proxy](https://oauth2-proxy.github.io/oauth2-proxy/)
- [Docker](https://www.docker.com/)

This `README.md` provides a comprehensive guide on setting up Google OAuth2, configuring the project, and running it using Docker Compose.
