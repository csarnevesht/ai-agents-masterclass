# Setting up pgvector in PostgreSQL

This guide will help you set up pgvector extension and create the embeddings table in your PostgreSQL database.

## Prerequisites

- Docker and Docker Compose are installed
- The local-ai-packaged containers are running
- pgAdmin is accessible at http://localhost:5050

## Setup Instructions

1. **Access pgAdmin**
   - Open your web browser and go to: `http://localhost:5050`
   - Login with:
     - Email: `admin@admin.com`
     - Password: `admin`

2. **Connect to PostgreSQL**
   - In pgAdmin, right-click on "Servers" in the left sidebar
   - Select "Register" > "Server"
   - In the "General" tab:
     - Name: `Local PostgreSQL` (or any name you prefer)
   - In the "Connection" tab:
     - Host name/address: `postgres`
     - Port: `5432`
     - Maintenance database: `postgres` (or your POSTGRES_DB value)
     - Username: Your POSTGRES_USER value
     - Password: Your POSTGRES_PASSWORD value

3. **Create Vector Extension and Embeddings Table**
   - Once connected, right-click on your database
   - Select "Query Tool"
   - Copy and paste the following SQL commands:
     ```sql
     CREATE EXTENSION IF NOT EXISTS vector;

     CREATE TABLE IF NOT EXISTS embeddings (
       id SERIAL PRIMARY KEY,
       embedding vector,
       text text,
       created_at timestamptz DEFAULT now()
     );
     ```
   - Click the "Execute" button (or press F5)

## Verification

To verify the setup:
1. In pgAdmin, expand your database
2. Expand "Extensions" - you should see `vector` listed
3. Expand "Tables" - you should see the `embeddings` table

## Troubleshooting

If you encounter any issues:
1. Make sure the PostgreSQL container is running
2. Verify your connection details in pgAdmin
3. Check that you have the correct permissions to create extensions and tables 