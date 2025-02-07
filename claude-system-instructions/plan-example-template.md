**Phase 1: Environment Setup**

1.  Create the main project directory and initialize the repository.

    *   Action: From the terminal, create a folder named `street_food_pipeline`.
    *   Directory: `/street_food_pipeline`
    *   Reference: PRD Section 1, Project Outline

2.  Set up a Python virtual environment using Python 3.11.4 (assuming prototype language).

    *   Action: Run `python3 -m venv venv` inside `/street_food_pipeline`.
    *   Validation: Execute `venv/bin/python --version` to confirm Python 3.11.4 is active.
    *   Reference: PRD Section 7, Tech Stack (prototype on macOS)

3.  Initialize a Git repository with `main` as the default branch.

    *   Action: Run `git init` and commit an initial README file.
    *   Directory: Root of project (`/street_food_pipeline`)
    *   Reference: PRD Section 1, Constraints

4.  Create a basic file structure:

    *   Action: Create folders `/backend`, `/config`, and `/tests`.
    *   Directory Structure: • `/street_food_pipeline/backend` • `/street_food_pipeline/config` • `/street_food_pipeline/tests`
    *   Reference: file_structure_document (from outline)

5.  Install required Python packages.

    *   Action: Create a `requirements.txt` in the project root with the following contents: requests schedule pyyaml sqlite3 (if needed, standard library in Python, else plan for an ORM like SQLAlchemy) cryptography # for encryption if required
    *   Command: Run `venv/bin/pip install -r requirements.txt`
    *   Reference: Tech Stack (macOS prototype, encryption protocols)

**Phase 2: Backend Development**

1.  Create the configuration file for pipeline settings.

    *   Action: Create file `/config/config.yaml` with contents:

2.  `apify_feed_url: 'https://api.apify.com/v2/your_feed_endpoint' # (adjust URL as needed) frequency_hours: 6 geographic_area: 'Greater Bristol, UK' database: type: 'sqlite' path: './database.db' encryption: enabled: true # include additional encryption configurations if needed`

    *   Reference: PRD Section 3; Project Outline (configurable geographic focus)

3.  Build the Apify feed client.

    *   Action: Create file `/backend/apify_client.py`.
    *   Implementation: Write a function `get_feed_data()` that: • Reads the Apify feed URL from `/config/config.yaml` (using PyYAML). • Makes an HTTP GET request using the `requests` library. • Returns the JSON response for further processing.
    *   Validation: Add a temporary test function in the file that prints the feed JSON and run it.
    *   Reference: PRD Section 4 (Data Retrieval Module)

4.  Develop the data parsing module to extract vendor information.

    *   Action: Create file `/backend/data_parser.py`.
    *   Implementation: Write functions to: • Identify if a post is from a street food vendor via criteria defined in the PRD (e.g., keywords in the description). • Extract details: serving times, location, food image URLs, menu details (text or image links) and reviews. • Return a structured Python dictionary with keys: handle, serving_time, location, images, menu, reviews, and metadata (timestamps etc.).
    *   Validation: Write a test script within `/tests/test_data_parser.py` that feeds sample JSON data and checks for expected outputs.
    *   Reference: PRD Section 4 (Data Extraction and Parsing)

5.  Build the database interface for data deduplication and storage.

    *   Action: Create file `/backend/db.py`.
    *   Implementation: Write functions to: • Create/connect to the SQLite database using the path from `/config/config.yaml`. • Create a table (if not exists) such as `vendors` with columns: id (primary key), handle (unique), serving_time, location, images (as JSON string or separate table reference), menu, reviews, last_updated timestamp, etc. • Insert new records or update existing vendor entries based on the unique social media handle. • If encryption is enabled (per config), use the `cryptography` library to encrypt sensitive fields (e.g., business or personal contact info if present).
    *   Directory: File location `/backend/db.py`
    *   Validation: Write unit tests in `/tests/test_db.py` to add and update a vendor record then query it.
    *   Reference: PRD Section 4 & 5 (Data Deduplication and Storage, Security)

6.  Create the scheduler module to run the pipeline on a fixed frequency.

    *   Action: Create file `/backend/scheduler.py`.
    *   Implementation: Use the `schedule` library to define a job that runs every 6 hours. • The job function should call `get_feed_data()` from the Apify client, process each post using the parser, and then update the database via the DB module.
    *   Validation: Run the scheduler in a test mode (short interval) and check logs to confirm the flow.
    *   Reference: PRD Section 3 (User Flow: scheduled every 6 hours)

7.  Tie all modules together in the main application file.

    *   Action: Create file `/backend/app.py`.
    *   Implementation: In `app.py`, perform the following steps: • Load configuration from `/config/config.yaml`. • Set up logging (e.g., write logs to stdout or a file in `/logs`). • Initialize the database (by invoking DB module's setup function). • Import and schedule the data retrieval job from `scheduler.py`. • Start the scheduler in a continuous loop (or indicate instructions for using a cron job if preferred).
    *   Validation: Run `venv/bin/python backend/app.py` and observe that the pipeline fetches data and processes it without error.
    *   Reference: PRD Sections 1 & 3 (Overall Flow and Core Pipeline Functionality)

**Phase 3: Integration**

1.  Integrate and test end-to-end pipeline execution on macOS.

    *   Action: Manually trigger the scheduled job by temporarily reducing the frequency interval (e.g., to every 1 minute) in `/config/config.yaml` for testing.
    *   Test: Monitor terminal output to verify data retrieval, parsing, deduplication, and database updates via log messages.
    *   Reference: PRD Section 3, Known Issues (ensuring data integrity and handling duplicates)

2.  Validate data encryption compliance:

    *   Action: For fields that require encryption, confirm using a test record that encryption and decryption functions operate as expected.
    *   Test: Write and run tests in `/tests/test_encryption.py` verifying that sensitive fields are correctly stored and retrieved using the `cryptography` library.
    *   Reference: PRD Section 5 and Non-Functional Requirements (Data Security & Compliance)

**Phase 4: Deployment Preparation**

1.  Document run instructions for the prototype on macOS.

    *   Action: Create a `README.md` in the project root that details: • Steps to set up the environment • How to run the pipeline (e.g., `venv/bin/python backend/app.py`) • How to run tests (`pytest` command in `/tests`)
    *   Reference: PRD Section 1 (Prototype Setup)

2.  (Optional) Containerize the application for future production scaling.

    *   Action: Create a `Dockerfile` in the project root. Basic steps: • Use a base image with Python 3.11.4 • Copy the project files • Install Python dependencies via `pip install -r requirements.txt` • Set the entrypoint to run `backend/app.py`
    *   Validation: Build the Docker image using `docker build -t street_food_pipeline .` and run it with `docker run street_food_pipeline`.
    *   Reference: PRD Section 7 (Scalability), Future Production needs

**Phase 5: Post-Launch**

1.  Set up monitoring and logging for the pipeline.

    *   Action: Integrate a logging library (if not already) to log errors, data retrieval successes, and other runtime metrics.
    *   File: Enhance `/backend/app.py` to log key events, optionally writing logs to `/logs/app.log`.
    *   Validation: Use a manual test run to generate and verify log entries match expected events.
    *   Reference: PRD Section 6 (Non-Functional Requirements: Robustness, Monitoring)

2.  Plan for future integration with additional processing pipelines (e.g., NLP sentiment analysis).

    *   Action: Document modular boundaries in code (e.g., the structured data returned by `data_parser.py`) so that further integration is straightforward.
    *   Reference: PRD Section 4 (Data Categorization and Storage) & Q&A (integration with analysis tools)

3.  (Maintenance) Schedule regular backups of the SQLite database if running as a persistent prototype.

    *   Action: Set up a cron job on macOS that copies `database.db` to a backup folder at the end of each day.
    *   Reference: PRD Section 7.3 (Post-Launch: Backups), Non-Functional Requirements (Scalability)

**Validation Summary**

*   Test each module individually with unit tests in `/tests` folder using pytest.
*   Run the main application to simulate a complete data retrieval and storage cycle.
*   Document edge-case handling (e.g., duplicate posts, missing data fields) within the parser module and validate through tests.
*   Reference test results in the `README.md`.

This completes the implementation plan for the street food vendor data pipeline prototype as described in the PRD. Each step is clearly documented and references the required PRD sections to ensure strict adherence to the design and functionality requirements.
