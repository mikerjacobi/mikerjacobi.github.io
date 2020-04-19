FROM node:13-alpine
ENV PUPPETEER_SKIP_CHROMIUM_DOWNLOAD=true
RUN mkdir /data && \
	apk --no-cache add git && \
    npm install -g puppeteer --unsafe-perm=true --allow-root && \
	npm install phantomjs-prebuilt@2.1.13 && \
	npm install -g resume-cli
RUN npm install -g jsonresume-theme-elegant 
RUN npm install -g jsonresume-theme-slick
RUN npm install -g jsonresume-theme-print-flexbox 
RUN npm install -g jsonresume-theme-so-moon 
RUN npm install -g jsonresume-theme-stackoverflow-es
RUN npm install -g jsonresume-theme-stackoverflow
RUN npm install -g jsonresume-theme-kendall
#RUN npm install -g jsonresume-theme-orbit-original
#RUN npm install -g jsonresume-theme-spartan-extended
#RUN npm install -g jsonresume-theme-kards
#RUN npm install -g jsonresume-theme-material
RUN npm install -g jsonresume-theme-eternal
RUN npm install -g jsonresume-theme-caffeine
RUN npm install -g jsonresume-theme-rocketspacer

# 1
RUN npm install -g jsonresume-theme-even 
RUN npm install -g jsonresume-theme-foxyboxy
#RUN npm install -g jsonresume-theme-md
#RUN npm install -g jsonresume-theme-simple-red
RUN npm install -g jsonresume-theme-a11y
RUN npm install -g jsonresume-theme-stackoverflow-skills
RUN npm install -g jsonresume-theme-samk
RUN npm install -g jsonresume-theme-short-nderkach
#RUN npm install -g jsonresume-theme-latex
#RUN npm install -g jsonresume-theme-standard-resume
RUN npm install -g jsonresume-theme-mint
RUN npm install -g jsonresume-theme-mix
RUN npm install -g jsonresume-theme-paper-v2
RUN npm install -g jsonresume-theme-paper-plus-plus
#RUN npm install -g jsonresume-theme-stackoverflow2
RUN npm install -g jsonresume-theme-sidepanel
#RUN npm install -g @tjscollins/jsonresume-theme-streamline
#RUN npm install -g jsonresume-theme-onepage-mrseanryan
RUN npm install -g jsonresume-theme-short-stephenfork
RUN npm install -g jsonresume-theme-short-with-location
RUN npm install -g jsonresume-theme-boilerplate
#2
RUN npm install -g jsonresume-theme-macchiato
#RUN npm install -g jsonresume-theme-moon
#RUN npm install -g jsonresume-theme-material-moon
RUN npm install -g jsonresume-theme-tan-responsive
RUN npm install -g jsonresume-theme-gross
#RUN npm install -g jsonresume-theme-kendall-gren
RUN npm install -g jsonresume-theme-pumpkin
RUN npm install -g jsonresume-theme-techlead
RUN npm install -g jsonresume-theme-mantra
RUN npm install -g jsonresume-theme-psimple
#RUN npm install -g jsonresume-theme-lowmess
RUN npm install -g jsonresume-theme-light-classy-concise
RUN npm install -g jsonresume-theme-eloquent
#RUN npm install -g jsonresume-theme-elegant
RUN npm install -g jsonresume-theme-mocha-responsive

WORKDIR /data
CMD bash
