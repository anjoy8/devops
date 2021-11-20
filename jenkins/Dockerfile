
# docker pull registry.cn-hangzhou.aliyuncs.com/bcvp/jenkins_with_dntcore3.1_5.0_6.0-cnpm_by_docker:latest
# docker run -u root --rm -d -p 3000:8080 --name jenkins -v /etc/localtime:/etc/localtime -v /usr/bin/docker:/usr/bin/docker -v /var/run/docker.sock:/var/run/docker.sock -v /home/dockerVolumes2/jenkins_home:/var/jenkins_home registry.cn-hangzhou.aliyuncs.com/bcvp/jenkins_with_dntcore3.1_5.0_6.0-cnpm_by_docker:latest
FROM jenkins/jenkins

# Switch to root to install .NET Core SDK
USER root

# Show distro information!
RUN uname -a && cat /etc/*release

# Based on instructiions at https://www.microsoft.com/net/download/linux-package-manager/debian9/sdk-current
# Install dependency for .NET Core
RUN apt-get update
RUN apt-get install -y curl libunwind8 gettext apt-transport-https

# Based on instructions at https://www.microsoft.com/net/download/linux-package-manager/debian9/sdk-current
# Install microsoft.qpg
RUN curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
RUN mv microsoft.gpg /etc/apt/trusted.gpg.d/microsoft.gpg
RUN sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-debian-stretch-prod stretch main" > /etc/apt/sources.list.d/dotnetdev.list'

# Install the .NET Core framework
RUN apt-get update
RUN apt-get install -y dotnet-sdk-3.1 \
	&& apt-get install -y dotnet-sdk-5.0 \ 
	&& apt-get install -y dotnet-sdk-6.0

# Install the npm 
RUN apt-get install -y curl \
  && curl -sL https://deb.nodesource.com/setup_14.x | bash - \
  && apt-get install -y nodejs \
  && curl -L https://www.npmjs.com/install.sh | sh
    
# Install cnpm
RUN npm install cnpm -g

RUN npm -v
RUN cnpm -v

# Switch back to the jenkins user.
USER jenkins
