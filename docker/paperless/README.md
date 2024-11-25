# Paperless

## Configuration

### 1. Adjust environment variables
Copy and rename the `example.env` to `.env` and adjust the variables inside this file.
Use `chmod 600 .env` afterwards.
For the `PAPERLESS_SECRET_KEY` generate a string with at least 50 characters (preferably longer) consisting of uppercase and lowercase letters, numbers, and special characters.
This secret key is used to generate the session keys.

### 2. Create folders
Create the folders configured in the `.env` file for using `mkdir db redis consume data export media`.

### 3. Adjust router rule
Replace the router rules for paperless in the `docker-compose.yml` file.
