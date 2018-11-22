# hadolint ignore=DL3007
FROM smartdevs/debian-stretch:latest
ARG DEBIAN_FRONTEND=noninteractive

ARG HADOLINT_VERSION=1.15.0
ARG HADOLINT_RUNTIME_REQUIREMENTS="libc6"
ARG HADOLINT_BUILD_REQUIREMENTS="curl"

# hadolint ignore=DL4006,DL3008,SC2086
RUN set -Eeu; \
    apt-get update -y; \
    apt-get install --no-install-recommends -y ${HADOLINT_RUNTIME_REQUIREMENTS:-} ${HADOLINT_EXTRA_RUNTIME_REQUIREMENTS:-} ${HADOLINT_BUILD_REQUIREMENTS} ${HADOLINT_EXTRA_BUILD_REQUIREMENTS:-}; \
    apt-mark auto ${HADOLINT_BUILD_REQUIREMENTS} ${HADOLINT_EXTRA_BUILD_REQUIREMENTS:-}; \
    curl -s -L -o /usr/local/bin/hadolint https://github.com/hadolint/hadolint/releases/download/v${HADOLINT_VERSION}/hadolint-Linux-x86_64; \
    chmod +x /usr/local/bin/hadolint; \
    curl -o /usr/local/bin/gitlab-helper -s https://s3.eu-central-1.amazonaws.com/valmano-gitlab-helper/gitlab-helper; \
    chmod +x /usr/local/bin/gitlab-helper; \
    apt-get purge --auto-remove -y; \
    dpkg -la | awk '{print $2}' | grep '\-dev' || true | xargs --no-run-if-empty apt-get remove -y; \
    apt-get clean; \
    apt-get --yes --quiet autoremove --purge; \
    find /var/log -type f -print0 | xargs -0 truncate -s0; \
    rm -rf \
        /var/lib/apt/lists/* \
        /tmp/* \
        /var/tmp/* \
        /usr/share/doc/* \
        /usr/share/groff/* \
        /usr/share/info/* \
        /usr/share/linda/* \
        /usr/share/lintian/* \
        /usr/share/man/*/* \
        ;
