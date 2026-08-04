FROM govpf/cypress:15.19

LABEL govpf.fromimage="govpf/cypress:15.19"
LABEL govpf.category="testing"

# Install Google Chrome
RUN set -eux; \
    apt-get update; \
    apt-get install -y --no-install-recommends \
        ca-certificates \
        curl \
        gnupg \
        dbus-x11 \
        zip; \
    \
    mkdir -p /etc/apt/keyrings; \
    curl -fsSL https://dl.google.com/linux/linux_signing_key.pub \
        | gpg --dearmor -o /etc/apt/keyrings/google.gpg; \
    \
    echo "deb [arch=amd64 signed-by=/etc/apt/keyrings/google.gpg] https://dl.google.com/linux/chrome/deb/ stable main" \
        > /etc/apt/sources.list.d/google-chrome.list; \
    \
    apt-get update; \
    apt-get install -y --no-install-recommends google-chrome-stable; \
    \
    rm -rf /var/lib/apt/lists/*

# "fake" dbus address to prevent errors
# https://github.com/SeleniumHQ/docker-selenium/issues/87
ENV DBUS_SESSION_BUS_ADDRESS=/dev/null

# Versions of local tools
RUN echo "node version:    $(node -v)" \
    && echo "npm version:     $(npm -v)" \
    && echo "yarn version:    $(yarn -v)" \
    && echo "debian version:  $(cat /etc/debian_version)" \
    && echo "Chrome version:  $(google-chrome --version)" \
    && echo "git version:     $(git --version)"

# Environment variables
ENV TERM=xterm
ENV npm_config_loglevel=warn
ENV npm_config_unsafe_perm=true