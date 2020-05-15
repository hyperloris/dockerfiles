FROM frolvlad/alpine-glibc:alpine-3.11_glibc-2.31
LABEL maintainer "Lorenzo Gigli <lorenzo.dramis@gmail.com>"

RUN apk add --no-cache \
    curl

ENV DENO_VERSION v1.0.0
ENV DENO_DOWNLOAD_URL "https://github.com/denoland/deno/releases/download/${DENO_VERSION}/deno-x86_64-unknown-linux-gnu.zip"

RUN curl --fail --location --output "deno.zip" ${DENO_DOWNLOAD_URL} \
    && unzip -o "deno.zip" \
    && chmod +x "deno" \
    && rm "deno.zip" \
    && mv deno /bin/deno

ENTRYPOINT [ "deno" ]
CMD [ "--help" ]
