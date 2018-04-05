# -----------------------------------------------------------------------------------------
# Start from Alpine OS with Oracle JDK8
# -----------------------------------------------------------------------------------------

FROM anapsix/alpine-java


# -----------------------------------------------------------------------------------------
# Install Python3
# -----------------------------------------------------------------------------------------

RUN apk add --no-cache python3
RUN python3 -m ensurepip
RUN rm -r /usr/lib/python*/ensurepip
RUN pip3 install --upgrade pip setuptools
RUN if [ ! -e /usr/bin/pip ]; then ln -s pip3 /usr/bin/pip ; fi
RUN if [[ ! -e /usr/bin/python ]]; then ln -sf /usr/bin/python3 /usr/bin/python; fi
RUN rm -r /root/.cache


# -----------------------------------------------------------------------------------------
# Install StaCoAn
# -----------------------------------------------------------------------------------------

RUN apk add --no-cache git
ADD https://api.github.com/repos/CarlNeuhaus/StaCoAn/git/refs/heads/master version.json
RUN git clone https://github.com/CarlNeuhaus/StaCoAn/
WORKDIR /StaCoAn/src
RUN pip3 install -r requirements.txt && chmod u+rwx /StaCoAn/src/jadx/bin/jadx

COPY stacoan.sh /stacoan.sh


# -----------------------------------------------------------------------------------------
# Expose us
# -----------------------------------------------------------------------------------------

EXPOSE 8000
EXPOSE 8080
ENTRYPOINT ["/bin/bash", "/stacoan.sh"]
