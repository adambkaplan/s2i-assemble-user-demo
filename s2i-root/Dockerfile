# s2i-root
FROM openshift/base-centos7

LABEL maintainer="Adam Kaplan <adam.kaplan@redhat.com>"

# TODO: Rename the builder environment variable to inform users about application you provide them
# ENV BUILDER_VERSION 1.0

LABEL io.k8s.description="Sample S2I builder as root assemble user" \
      io.k8s.display-name="S2I Root Assemble User App" \
      io.openshift.s2i.assemble-user="root" 

# TODO (optional): Copy the builder files into /opt/app-root
# COPY ./<builder_folder>/ /opt/app-root/

# TODO: Copy the S2I scripts to /usr/libexec/s2i, since openshift/base-centos7 image
# sets io.openshift.s2i.scripts-url label that way, or update that label
COPY ./s2i/bin/ /usr/libexec/s2i

RUN chown -R 1001:1001 /opt/app-root

# This default user is created in the openshift/base-centos7 image
USER 1001

CMD ["/usr/libexec/s2i/usage"]
