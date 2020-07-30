FROM cloudbees/java-with-docker-client
ENV JDK_VERSION=7u95 \
    JDK_PATH=jdk1.7.0_95 \
    NEXUS=http://xxxxxxxxxxxxx/ \
### Environment variable node and npm
    NODE_VERSION=v10.16.0 \
    NPM=6.10.2


# change to tmp folder
WORKDIR /root

# Download and extract jdk to opt folder
RUN wget --no-check-certificate --no-cookies ${NEXUS}/jdk/jdk-${JDK_VERSION}-linux-x64.tar.gz \      
&& tar -zvxf jdk-${JDK_VERSION}-linux-x64.tar.gz -C /opt/ \    
&& ln -s /opt/jdk-${JDK_VERSION}-linux-x64 /opt/${JDK_PATH} \    
&& rm -f jdk-${JDK_VERSION}-linux-x64.tar.gz 


# Install NODE

RUN wget --no-check-certificate --no-cookies ${NEXUS}/node/node/${NODE_VERSION}/node-${NODE_VERSION}-linux-x64.tar.xz && \
	tar -xvf node-${NODE_VERSION}-linux-x64.tar.xz -C /opt/ && \
	ln -s /opt/node-${NODE_VERSION}-linux-x64 /opt/node && \
	rm -rf node-${NODE_VERSION}-linux-x64.tar.xz
	
# add executables to path    
RUN update-alternatives --install "/usr/bin/node" "node" "/opt/node/bin/node" 1 && \
    update-alternatives --set "node" "/opt/node/bin/node" 
# add executables to path    
RUN update-alternatives --install "/usr/bin/npm" "npm" "/opt/node/bin/npm" 1 && \
    update-alternatives --set "npm" "/opt/node/bin/npm" 

# Install Angular and Angular-CLI
RUN npm config set registry http://xxxxxxxxxxx/repository// 
### Set NPM Environment
RUN mkdir npm-global; chmod -R 777 npm-global && \
    npm config set prefix '/root/npm-global' 
    
ENV PATH=$PATH:/root/npm-global/bin
RUN npm install -g angular
RUN cd /root/npm-global/lib/node_modules;npm install node-sass && \
    npm install @angular/cli@latest && \
    npm install @angular-devkit/core && \
    npm i @bellese/angular-design-system
# change to root folder
RUN ng --version
RUN npm config delete proxy
WORKDIR /root
