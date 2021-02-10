Waiting for build to start...
Picked Git content provider.
Cloning into '/tmp/repo2dockeramo6i3l9'...
HEAD is now at d531ef3 Create test.ipynb
Building conda environment for python=3.7Using PythonBuildPack builder
Building conda environment for python=3.7Building conda environment for python=3.7Step 1/45 : FROM buildpack-deps:bionic
 ---> 17c4791bcf21
Step 2/45 : ENV DEBIAN_FRONTEND=noninteractive
 ---> Using cache
 ---> 8b3cccf1082b
Step 3/45 : RUN apt-get -qq update &&     apt-get -qq install --yes --no-install-recommends locales > /dev/null &&     apt-get -qq purge &&     apt-get -qq clean &&     rm -rf /var/lib/apt/lists/*
 ---> Using cache
 ---> 122bc7d70e2d
Step 4/45 : RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen &&     locale-gen
 ---> Using cache
 ---> 96f9c81fec49
Step 5/45 : ENV LC_ALL en_US.UTF-8
 ---> Using cache
 ---> 44e8cdb26712
Step 6/45 : ENV LANG en_US.UTF-8
 ---> Using cache
 ---> bbac306cff4a
Step 7/45 : ENV LANGUAGE en_US.UTF-8
 ---> Using cache
 ---> 0e99cf9f14e9
Step 8/45 : ENV SHELL /bin/bash
 ---> Using cache
 ---> a75c47fe7ae2
Step 9/45 : ARG NB_USER
 ---> Using cache
 ---> 321bf3f7c1d0
Step 10/45 : ARG NB_UID
 ---> Using cache
 ---> 23e276238122
Step 11/45 : ENV USER ${NB_USER}
 ---> Using cache
 ---> 241839c2cb33
Step 12/45 : ENV HOME /home/${NB_USER}
 ---> Using cache
 ---> ffc7581ea585
Step 13/45 : RUN groupadd         --gid ${NB_UID}         ${NB_USER} &&     useradd         --comment "Default user"         --create-home         --gid ${NB_UID}         --no-log-init         --shell /bin/bash         --uid ${NB_UID}         ${NB_USER}
 ---> Using cache
 ---> d8e3be1df5fd
Step 14/45 : RUN wget --quiet -O - https://deb.nodesource.com/gpgkey/nodesource.gpg.key |  apt-key add - &&     DISTRO="bionic" &&     echo "deb https://deb.nodesource.com/node_14.x $DISTRO main" >> /etc/apt/sources.list.d/nodesource.list &&     echo "deb-src https://deb.nodesource.com/node_14.x $DISTRO main" >> /etc/apt/sources.list.d/nodesource.list
 ---> Using cache
 ---> 1c6b42ac8d84
Step 15/45 : RUN apt-get -qq update &&     apt-get -qq install --yes --no-install-recommends   less        nodejs        unzip        > /dev/null &&     apt-get -qq purge &&     apt-get -qq clean &&     rm -rf /var/lib/apt/lists/*
 ---> Using cache
 ---> fc5afc14d69c
Step 16/45 : EXPOSE 8888
 ---> Using cache
 ---> 44bd3cb8aba3
Step 17/45 : ENV APP_BASE /srv
 ---> Using cache
 ---> 2042b0fd9c48
Step 18/45 : ENV NPM_DIR ${APP_BASE}/npm
 ---> Using cache
 ---> 9bfbcdc64f80
Step 19/45 : ENV NPM_CONFIG_GLOBALCONFIG ${NPM_DIR}/npmrc
 ---> Using cache
 ---> f58a227ae53d
Step 20/45 : ENV CONDA_DIR ${APP_BASE}/conda
 ---> Using cache
 ---> 159ab89c47df
Step 21/45 : ENV NB_PYTHON_PREFIX ${CONDA_DIR}/envs/notebook
 ---> Using cache
 ---> cf475e9e3152
Step 22/45 : ENV KERNEL_PYTHON_PREFIX ${NB_PYTHON_PREFIX}
 ---> Using cache
 ---> f7e9c8256972
Step 23/45 : ENV PATH ${NB_PYTHON_PREFIX}/bin:${CONDA_DIR}/bin:${NPM_DIR}/bin:${PATH}
 ---> Using cache
 ---> da2d61f9dd13
Step 24/45 : COPY --chown=1000:1000 build_script_files/-2fusr-2flib-2fpython3-2e8-2fsite-2dpackages-2frepo2docker-2fbuildpacks-2fconda-2factivate-2dconda-2esh-391af5 /etc/profile.d/activate-conda.sh
 ---> Using cache
 ---> 37146df4f615
Step 25/45 : COPY --chown=1000:1000 build_script_files/-2fusr-2flib-2fpython3-2e8-2fsite-2dpackages-2frepo2docker-2fbuildpacks-2fconda-2fenvironment-2epy-2d3-2e7-2efrozen-2eyml-037262 /tmp/environment.yml
 ---> Using cache
 ---> 514920f1247b
Step 26/45 : COPY --chown=1000:1000 build_script_files/-2fusr-2flib-2fpython3-2e8-2fsite-2dpackages-2frepo2docker-2fbuildpacks-2fconda-2finstall-2dminiforge-2ebash-514214 /tmp/install-miniforge.bash
 ---> Using cache
 ---> b9c408ed8f8b
Step 27/45 : RUN mkdir -p ${NPM_DIR} && chown -R ${NB_USER}:${NB_USER} ${NPM_DIR}
 ---> Using cache
 ---> 49ce608ff931
Step 28/45 : USER ${NB_USER}
 ---> Using cache
 ---> 9c2fc4f2f83a
Step 29/45 : RUN npm config --global set prefix ${NPM_DIR}
 ---> Using cache
 ---> 4f133871a3f1
Step 30/45 : USER root
 ---> Using cache
 ---> af5a30068dbe
Step 31/45 : RUN TIMEFORMAT='time: %3R' bash -c 'time /tmp/install-miniforge.bash' && rm /tmp/install-miniforge.bash /tmp/environment.yml
 ---> Using cache
 ---> f228bebd6a96
Step 32/45 : ARG REPO_DIR=${HOME}
 ---> Using cache
 ---> 5c56413d5d60
Step 33/45 : ENV REPO_DIR ${REPO_DIR}
 ---> Using cache
 ---> 967951b0fb02
Step 34/45 : WORKDIR ${REPO_DIR}
 ---> Using cache
 ---> f9763271572d
Step 35/45 : RUN chown ${NB_USER}:${NB_USER} ${REPO_DIR}
 ---> Using cache
 ---> b8f80ca9d5cd
Step 36/45 : ENV PATH ${HOME}/.local/bin:${REPO_DIR}/.local/bin:${PATH}
 ---> Using cache
 ---> 55758abe88c3
Step 37/45 : ENV CONDA_DEFAULT_ENV ${KERNEL_PYTHON_PREFIX}
 ---> Using cache
 ---> 7197467df63a
Step 38/45 : COPY --chown=1000:1000 src/ ${REPO_DIR}
 ---> 000e0a23a40b
Step 39/45 : LABEL repo2docker.ref="d531ef33b868801d886dbaa534960488bc203330"
 ---> Running in 7ca3e9b92da4
Removing intermediate container 7ca3e9b92da4
 ---> 09e98501cd4d
Step 40/45 : LABEL repo2docker.repo="https://github.com/KJokisch/udemy"
 ---> Running in de78c046dea6
Removing intermediate container de78c046dea6
 ---> c7cd0c7e313b
Step 41/45 : LABEL repo2docker.version="2021.01.0+16.gcb4621f"
 ---> Running in 58fd269bf117
Removing intermediate container 58fd269bf117
 ---> 72f441345bc6
Step 42/45 : USER ${NB_USER}
 ---> Running in e752dbba9be8
Removing intermediate container e752dbba9be8
 ---> 43b4f3f295f2
Step 43/45 : COPY /repo2docker-entrypoint /usr/local/bin/repo2docker-entrypoint
 ---> 332938db09f8
Step 44/45 : ENTRYPOINT ["/usr/local/bin/repo2docker-entrypoint"]
 ---> Running in 4909f2b7a650
Removing intermediate container 4909f2b7a650
 ---> 210db9d31805
Step 45/45 : CMD ["jupyter", "notebook", "--ip", "0.0.0.0"]
 ---> Running in 7e68ae3aad3e
Removing intermediate container 7e68ae3aad3e
 ---> b7c487e6cfec
{"aux": {"ID": "sha256:b7c487e6cfecb82d4c8c925698747b76028c8a805c06c05e02a539a00f17a403"}}Successfully built b7c487e6cfec
Successfully tagged gcr.io/binderhub-288415/r2d-staging-72d7634-kjokisch-2dudemy-72fd83:d531ef33b868801d886dbaa534960488bc203330
Successfully pushed gcr.io/binderhub-288415/r2d-staging-72d7634-kjokisch-2dudemy-72fd83:d531ef33b868801d886dbaa534960488bc203330Built image, launching...
Launching server...
server running at https://hub.gke2.mybinder.org/user/kjokisch-udemy-uq125130/
