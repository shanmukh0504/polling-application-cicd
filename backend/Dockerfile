# Use a Rust base image with Cargo installed
FROM rust AS builder

# Set the working directory inside the container
WORKDIR /usr/src/app

# Copy the Cargo.toml and Cargo.lock files
COPY Cargo.toml Cargo.lock ./

# Now copy the source code
COPY ./src ./src

ARG MONGODB_URI
ARG JWT_SECRET
ARG ORIGIN

# Set environment variables
ENV MONGODB_URI=${MONGODB_URI}
ENV JWT_SECRET=${JWT_SECRET}
ENV ORIGIN=${ORIGIN}

RUN touch .env
# Create .env file and write database URL and JWT secret
RUN echo "MONGODB_URI=${MONGODB_URI}" > .env && echo "JWT_SECRET=${JWT_SECRET}" >> .env && echo "ORIGIN=${ORIGIN}" >> .env

# apt install libssl-dev and openssl
RUN apt-get update && apt-get install -y libssl-dev openssl


RUN cat .env && echo "Environment variables set"

# Build your application
RUN cargo build --release

CMD [ "cargo","run","--release" ]