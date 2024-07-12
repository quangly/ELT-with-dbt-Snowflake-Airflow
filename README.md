# ELT-with-dbt-Snowflake-Airflow
ELT with dbt, Snowflake, Airflow


# Setup Python Virtual Environment

    python -m venv myenv
    source myenv/bin/activate
    pip install -r requirements.txt

# Steps
    1. Setup Snowflake environment
    2. Configure dbt_profile.yml
    3. Create source and staging files
    4. Macros (DRY Principle)
    5. Transform models (facts, tables, data marts)
    6. Generic and Singular Tests
    7. Deploy on Airflow


# Step 1: Setup snowflake environment

    -- create accounts
    use role accountadmin;

    create warehouse dbt_wh with warehouse_size='x-small';
    create database if not exists dbt_db;
    create role if not exists dbt_role;

    show grants on warehouse dbt_wh;

    grant role dbt_role to user [snowflake_user];
    grant usage on warehouse dbt_wh to role dbt_role;
    grant all on database dbt_db to role dbt_role;

    use role dbt_role;

    create schema if not exists dbt_db.dbt_schema;

    -- clean up
    use role accountadmin;

    drop warehouse if exists dbt_wh;
    drop database if exists dbt_db;
    drop role if exists dbt_role;