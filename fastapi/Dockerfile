# Use a base image with PyPy and Python pre-installed
FROM pypy:slim

# Install dependencies required for Rust and Cargo
RUN apt-get update && apt-get install -y \
    curl \
    build-essential

# Install Rust
RUN curl https://sh.rustup.rs -sSf | sh -s -- -y

# Add Cargo binaries to PATH
ENV PATH="/root/.cargo/bin:${PATH}"

# Copy the requirements.txt
COPY requirements.txt /usr/src/requirements.txt

# RUN pip install --upgrade pip
RUN pip install -r /usr/src/requirements.txt

# Copy the app folder
COPY ./app /app

# add a non-root user to run the app
RUN useradd nonrootuser

# switch to non-root user
USER nonrootuser

# Specify the default command to run when the container starts
CMD ["pypy3", "-m", "uvicorn", "app.main:app", "--port", "8080"]

# Expose port
EXPOSE 8080/tcp