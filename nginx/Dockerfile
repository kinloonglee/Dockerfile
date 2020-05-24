FROM centos:centos7.6.1810
RUN  yum install -y gcc gcc-c++ make   openssl-devel pcre-devel gd-devel  \
	        iproute net-tools telnet wget curl build-essential libc6 \
	       	libpcre3 libpcre3-dev libpcrecpp0 libssl0.9.8 libssl-dev \
		#zlib1g zlib1g-dev lsb-base openssl libssl-dev  libgeoip1 \
		libgeoip-dev  google-perftools libgoogle-perftools-dev \
		libperl-dev  libgd2-xpm-dev libatomic-ops-dev libxml2-dev \
		libxslt1-dev python-dev  unzip  && \
                mkdir -p  /nginx/{log,run,conf,sbin}   && \
                mkdir -p  /nginx/cache/{client_temp,proxy_temp,fastcgi_temp,uwsgi_temp,scgi_temp}   && \
                yum clean all && \
                rm -rf /var/cache/yum/*

COPY source  /
RUN tar zxf nginx-1.18.0.tar.gz &&  tar xf openssl-1.0.2k.tar.gz && unzip echo-nginx-module-master.zip && unzip ngx_http_substitutions_filter_module-master.zip && \
    cd nginx-1.18.0 && \
         ./configure --prefix=/nginx \    
	 --sbin-path=/nginx/sbin/nginx  \   
	 --conf-path=/nginx/conf/nginx.conf   \  
	 --error-log-path=/nginx/log/error.log   \  
	 --http-log-path=/nginx/log/access.log   \  
	 --pid-path=/nginx/run/nginx.pid     \
	 --lock-path=/nginx/run/nginx.lock   \  
	 --http-client-body-temp-path=/nginx/cache/client_temp   \  
	 --http-proxy-temp-path=/nginx/cache/proxy_temp     \
	 --http-fastcgi-temp-path=/nginx/cache/fastcgi_temp   \  
	 --http-uwsgi-temp-path=/nginx/cache/uwsgi_temp     \
	 --http-scgi-temp-path=/nginx/cache/scgi_temp     \
	 --with-http_ssl_module     \
	 --with-http_realip_module     \
	 --with-http_addition_module    \ 
	 --with-http_sub_module     \
	 --with-http_dav_module    \ 
	 --with-http_flv_module     \
	 --with-http_mp4_module     \
	 --with-http_gunzip_module    \ 
	 --with-http_gzip_static_module \    
	 --with-http_random_index_module   \  
	 --with-http_secure_link_module     \
	 --with-http_stub_status_module     \
	 --with-http_auth_request_module    \ 
	 --with-threads     \
	 --with-stream     \
	 --with-stream_ssl_module   \  
	 --with-http_slice_module    \ 
	 --with-mail     \
	 --with-mail_ssl_module     \
	 --with-file-aio     \
	 --with-http_v2_module \
	 --with-openssl=../openssl-1.0.2k \
	 --add-module=../ngx_http_substitutions_filter_module-master \
	 --add-module=../echo-nginx-module-master && make && make install \
	 && ln -sf /nginx/sbin/nginx   /usr/sbin/nginx
CMD ["nginx","-g","daemon off;"]
