# HeyForm Portainer Stack

This repo is set up for Portainer's `Deploy from Git repository` flow.

## Files

- `docker-compose.yml`: Portainer-ready stack for HeyForm, MongoDB, and KeyDB
- `.env.example`: environment variables you can copy into Portainer or into a local `.env`

## Portainer deployment

1. Push this repo to GitHub, GitLab, or another Git server Portainer can reach.
2. In Portainer, open `Stacks`.
3. Choose `Add stack`.
4. Choose `Git Repository`.
5. Set the repository URL to this repo.
6. Set the compose path to `docker-compose.yml`.
7. Add these environment variables in Portainer before deploying:
   - `APP_HOMEPAGE_URL`
   - `SESSION_KEY`
   - `FORM_ENCRYPTION_KEY`
8. Deploy the stack.

## Recommended values

- `APP_HOMEPAGE_URL=https://forms.example.com` if you will expose it behind a reverse proxy
- `SESSION_KEY` and `FORM_ENCRYPTION_KEY`: generate long random strings, for example with `openssl rand -hex 32`

## Notes

- This stack was validated locally on March 12, 2026 with `heyform/community-edition:latest`, `percona/percona-server-mongodb:4.4`, and `eqalpha/keydb:latest`.
- Uploaded files, MongoDB data, and KeyDB data are stored in Docker named volumes.
- The stack publishes HeyForm on port `9513` by default. Change `HEYFORM_HOST_PORT` if needed.
- HeyForm itself serves plain HTTP on port `8000` inside the container. For HTTPS, place it behind a reverse proxy.
- This stack follows HeyForm's simple upstream pattern and keeps MongoDB private on the internal Docker network without database auth enabled.
- The previous `eqalpha/keydb:6.3.3` tag no longer resolves on Docker Hub; use `eqalpha/keydb:latest` unless you have a known-good pinned tag.
