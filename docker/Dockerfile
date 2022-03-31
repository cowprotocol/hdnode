FROM docker.io/library/rust:1-bullseye as build

WORKDIR /src/hdnode

COPY Cargo.* .
COPY src/ src/
RUN cargo build --release


FROM docker.io/library/debian:bullseye-slim

COPY --from=build /src/hdnode/target/release/hdnode /opt/hdnode/
COPY Rocket.toml /opt/hdnode/
COPY validators/ /opt/hdnode/validators/

ENV ROCKET_CONFIG=/opt/hdnode/Rocket.toml
ENV ROCKET_PROFILE=docker
EXPOSE 9545

CMD ["/opt/hdnode/hdnode"]
