# ---------------------------------------------------------
# MariaDB Yolk for Pterodactyl
#
# MariaDB is a community-developed, commercially supported
# fork of the MySQL relational database management system,
# intended to remain free and open-source software under
# the GNU General Public
#
# ---------------------------------------------------------

FROM        --platform=$TARGETOS/$TARGETARCH mariadb:11.8

LABEL       author="Daniel Barton" maintainer="danielb@purpleflaghosting.com"

ENV         DEBIAN_FRONTEND=noninteractive

RUN         apt update -y && apt install -y libnss-wrapper gettext-base
RUN 		useradd -d /home/container -m container -s /bin/bash


## Prepare NSS Wrapper for the entrypoint
ENV         NSS_WRAPPER_PASSWD=/tmp/passwd NSS_WRAPPER_GROUP=/tmp/group
COPY		--chown=root:root --chmod=644 nss/passwd.template nss/group.template /


USER        container
ENV         USER=container HOME=/home/container
WORKDIR     /home/container


COPY		--chown=root:root --chmod=755 ../entrypoint.sh /entrypoint.sh
ENTRYPOINT	["/entrypoint.sh"]
