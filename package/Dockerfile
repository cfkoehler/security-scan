FROM ubuntu:18.04

ARG kube_bench_tag=v0.0.27-rancher-1
#ARG kube_bench_source_code_tag=0.0.28
ARG sonobuoy_version=0.14.2

RUN apt-get update && apt-get install -y curl jq
RUN curl -sLf https://storage.googleapis.com/kubernetes-release/release/v1.13.5/bin/linux/amd64/kubectl > /usr/local/bin/kubectl-1.13 \
    && ln -sv /usr/local/bin/kubectl-1.13 /usr/local/bin/kubectl \
    && chmod +x /usr/local/bin/kubectl*
RUN curl -sLf https://github.com/heptio/sonobuoy/releases/download/v${sonobuoy_version}/sonobuoy_${sonobuoy_version}_linux_amd64.tar.gz | tar -xvzf - -C /usr/bin sonobuoy
#RUN curl -sLf https://github.com/aquasecurity/kube-bench/releases/download/${kube_bench_tag}/kube-bench_${kube_bench_source_code_tag}_linux_amd64.tar.gz | tar -xvzf - -C /usr/bin
RUN curl -sLf https://github.com/leodotcloud/kube-bench/releases/download/${kube_bench_tag}/kube-bench.tar.gz | tar -xvzf - -C /usr/bin

COPY package/cfg/ /cfg/
COPY package/run.sh \
     package/run_sonobuoy_plugin.sh \
     bin/kube-bench-summarizer \
     package/helper_scripts/check_files_permissions.sh \
     package/helper_scripts/check_files_owner_in_dir.sh \
     /usr/bin/

CMD ["run.sh"]