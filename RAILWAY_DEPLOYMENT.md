# Deploy on Railway

This project uses the included Dockerfile. It installs FFmpeg, installs the Python dependencies, and starts FastAPI on Railway's assigned `PORT`.

## Deploy from GitHub

1. Create a private GitHub repository and upload the project files. Keep `.env`, `youtube_client_secret.json`, and everything inside `secrets/` out of Git. The included `.gitignore` excludes them.
2. In Railway, create a project and choose **Deploy from GitHub repo**. Select this repository; Railway detects and builds the Dockerfile.
3. In the Railway service's **Variables**, add `GEMINI_API_KEY` with your own key. Optionally set `GEMINI_MODEL`; it defaults to `gemini-3.1-flash-lite`. `YOUTUBE_AUTH_ENABLED` defaults to `0`, so YouTube OAuth is inactive for demo use.
4. Deploy and wait for the build to finish. Check `/health` on the service to confirm the app starts.
5. Open the service's **Settings → Networking → Public Networking**, choose **Generate Domain**, and share the resulting `*.up.railway.app` URL.

Do not upload your local `.env` or paste its key into GitHub. Add secrets through Railway Variables. Railway deployments from a linked GitHub branch rebuild when new commits are pushed.

## Demo notes

Anyone with the public URL can open the app. The demo does not require Google or YouTube sign-in. Uploaded videos and generated files are stored by the app under its working directory; configure persistent storage before relying on them across redeployments. Avoid using the public demo for private videos because this project does not provide per-user accounts.
