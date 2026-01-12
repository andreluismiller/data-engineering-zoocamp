# base Docker image
FROM python:3.13.11
# Copy uv binary from official uv image (multi-stage build pattern)
COPY --from=ghcr.io/astral-sh/uv:latest /uv /bin/

# working directory inside container
WORKDIR /code
# Add virtual environment to PATH so we can use installed packages
ENV PATH="/code/.venv/bin:$PATH"

# Copy dependency files first (better layer caching)
COPY "pyproject.toml" "uv.lock" ".python-version" ./

# Install dependencies from lock file (ensures reproducible builds)
RUN uv sync --locked

#copy script inside container
COPY pipeline.py .

# set entry point
ENTRYPOINT ["python", "pipeline.py"]