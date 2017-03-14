
# start from debian base image with skope user and group defined 
FROM  openskope/base

ARG DEBIAN_FRONTEND=noninteractive

USER root

RUN echo '****** Install Java 8 Runtime Environment'                                                \
 && apt-get -y install default-jre                                                                  \
                                                                                                    \
 && echo '***** Install graphviz for visualizing RestFlow workflows *****'                          \
 && apt-get -y install graphviz                                                                     \
                                                                                                    \
 && echo "***** install latest verison of R to support the R actor *****"                           \
 && echo deb http://cran.rstudio.com/bin/linux/ubuntu xenial/ > /etc/apt/sources.list.d/cran.list   \
 && gpg --keyserver keyserver.ubuntu.com --recv-key E084DAB9                                        \
 && gpg -a --export E084DAB9 |  apt-key add -                                                       \
 && apt-get -y update                                                                               \
 && apt-get -y install r-base                                                                       \
                                                                                                    \
 && echo '***** install R packages for RestFlow R actor *****'                                      \
 && echo 'install.packages(c("optparse", "rjson"), repos="http://cran.us.r-project.org")'           \
    > /tmp/install_r_packages_for_restflow.R                                                        \
 && R --no-save < /tmp/install_r_packages_for_restflow.R                                            \
                                                                                                    \
 && echo '***** Install Python2, Python3, and pip for both to support the Python actor *****'       \
 && apt-get -y install python python-pip python3 python3-pip                                        \
 && pip2 install --upgrade pip                                                                      \
 && pip3 install --upgrade pip                                                                      \
                                                                                                    \
 && echo '***** Download skope-restflow executable jar *****'                                       \
    && mkdir ~skope/bin                                                                             \
    && wget -O ~skope/bin/skope-restflow.jar https://github.com/openskope/skope-restflow/releases/download/v1.1.0/skope-restflow-1.1.0-jar-with-dependencies.jar

USER skope

ENTRYPOINT ["java", "-jar", "/home/skope/bin/skope-restflow.jar"]



