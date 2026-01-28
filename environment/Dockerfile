# hash:sha256:dee1dc841f2a611b93deaae04f9e07b573ddc716839134f927ca1016a0b7b0c1
ARG REGISTRY_HOST
FROM $REGISTRY_HOST/codeocean/mambaforge3:24.5.0-0-python3.12.4-ubuntu22.04

ARG DEBIAN_FRONTEND=noninteractive
ARG GIT_ASKPASS
COPY git-askpass /

RUN --mount=type=secret,id=git-access-token \
    GIT_ACCESS_TOKEN="$(cat /run/secrets/git-access-token)" \
    pip install -U --no-cache-dir \
    boto3==1.43.30 \
    pydantic-settings==2.9.1 \
    s3fs==2026.1.0 \
    -e git+https://github.com/AllenNeuralDynamics/analysis-pipeline-utils@feat-skip-in-dispatch#egg=analysis-pipeline-utils

COPY postInstall /
RUN --mount=type=secret,id=secrets . /run/secrets/secrets \
    && /postInstall
