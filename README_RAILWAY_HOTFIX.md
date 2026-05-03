# Railway Build Hotfix

Use this package if Railway fails during `Build image`.

Most common causes:
1. Railway is building from the wrong folder. Dockerfile must be in the selected repo root.
2. MediaPipe/OpenCV wheels fail on Python 3.11/3.12 in some environments.
3. Missing system libraries needed by OpenCV/MediaPipe.

This hotfix uses:
- `python:3.10-slim-bookworm`
- extra OpenCV/MediaPipe system libraries
- `protobuf<5`
- explicit `./Dockerfile` path in `railway.json`

## Railway variables

Set in the API service:

```env
DATABASE_URL=${{Postgres.DATABASE_URL}}
BEFORMA_API_KEY=your-secret-key
ALLOWED_ORIGINS=*
INIT_DB_ON_STARTUP=true
BEFORMA_MAX_UPLOAD_MB=200
BEFORMA_SESSION_TTL_SECONDS=3600
```

## Important repo structure

Upload the CONTENTS of this folder to GitHub root, not the folder itself.

Correct:

```text
repo-root/
  main.py
  Dockerfile
  requirements.txt
  railway.json
```

Wrong:

```text
repo-root/
  beforma_railway_api_package_hotfix/
    main.py
    Dockerfile
```

If you keep the nested folder, set Railway Root Directory to `beforma_railway_api_package_hotfix`.
