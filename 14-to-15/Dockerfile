#
# NOTE: THIS DOCKERFILE IS GENERATED VIA "apply-templates.sh"
#
# PLEASE DO NOT EDIT IT DIRECTLY.
#

FROM postgres:15-bookworm

RUN sed -i 's/$/ 14/' /etc/apt/sources.list.d/pgdg.list

RUN set -eux; \
	apt-get update; \
	apt-get install -y --no-install-recommends \
		postgresql-14='14.18-1.pgdg120+1' \
	; \
	rm -rf /var/lib/apt/lists/*

ENV PGBINOLD=/usr/lib/postgresql/14/bin
ENV PGBINNEW=/usr/lib/postgresql/15/bin

ENV PGDATAOLD=/var/lib/postgresql/14/data
ENV PGDATANEW=/var/lib/postgresql/15/data

RUN set -eux; \
	mkdir -p "$PGDATAOLD" "$PGDATANEW"; \
	chown -R postgres:postgres /var/lib/postgresql

WORKDIR /var/lib/postgresql

COPY docker-upgrade /usr/local/bin/

ENTRYPOINT ["docker-upgrade"]

# recommended: --link
CMD ["pg_upgrade"]
