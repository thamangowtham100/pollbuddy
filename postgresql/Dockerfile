# syntax=docker/dockerfile:1.5.1
FROM base

ARG TARGETARCH

EXPOSE 5432

# Platform specific does require arch specific identifier.
RUN --mount=type=cache,id=postgresql-apk-${TARGETARCH},sharing=locked,target=/var/cache/apk \
    apk add \
        postgresql \
        postgresql-client \
    && \
    mkdir -p /var/lib/postgresql/data /etc/postgresql && \
    chown -R postgres:postgres /var/lib/postgresql && \
    chmod 700 /var/lib/postgresql/data && \
    cleanup.sh

ENV \
    PGDATA=/var/lib/postgresql/data

COPY --link rootfs /
