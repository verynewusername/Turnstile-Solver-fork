FROM ubuntu:latest

# --- Environment and Locale Setup (No changes needed) ---
ENV DEBIAN_FRONTEND=noninteractive
ENV LANG=en_US.UTF-8
ENV LANGUAGE=en_US:en
ENV LC_ALL=en_US.UTF-8
ENV TZ=America/New_York
ENV RUN_API_SOLVER=false

# --- Locale and Timezone Configuration (No changes needed) ---
RUN apt-get update && \
    apt-get -y upgrade && \
    apt-get install -y --no-install-recommends tzdata locales && \
    sed -i '/en_US.UTF-8/s/^# //g' /etc/locale.gen && \
    locale-gen && \
    ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone && \
    echo "LC_ALL=en_US.UTF-8" >> /etc/environment && \
    echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen && \
    echo "LANG=en_US.UTF-8" > /etc/locale.conf && \
    locale-gen en_US.UTF-8

# --- Install Dependencies and Clean Up ---
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    git \
    curl \
    wget \
    screen \
    sudo \
    xrdp \
    xfce4 \
    xorgxrdp \
    dbus-x11 \
    xfce4-terminal \
    python3-pip \
    ca-certificates \
    xvfb \
    # ================================================================= #
    # MODIFICATION: Replaced amd64 Google Chrome with arm64 Chromium. #
    # This is the key change for Raspberry Pi compatibility.            #
    chromium-browser \
    # ================================================================= #
    && \
    # Clean up to reduce final image size
    apt remove -y light-locker xscreensaver && \
    apt autoremove -y && \
    rm -rf /var/lib/apt/lists/*

# --- Copy and Execute Run Script (No changes needed) ---
COPY ./run.sh /usr/bin/
RUN chmod +x /usr/bin/run.sh

EXPOSE 3389
ENTRYPOINT ["/usr/bin/run.sh"]
